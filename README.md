# sfdx-playground

> Simulation of various scenarios of a Salesforce development process

This repo is mainly used for testing `force-dev-tool changeset create`.

**WARNING: The existing commits of this repository will be rewritten from time to time in order to create a clean history.**

## Introduction

* Every scenario lives in its own branch.
* A `README.md` file in the branch describes the intention of the scenario.
* The commit history tells the story of every step.

## Contributing

Fork and clone this repo.

```console
$ git checkout --orphan myscenario && echo "" > README.md && git add -A . && git commit -m "v0: initial commit"
```

Develop and commit each step. Prefix commit messages with version names, e.g. `v1: add initial apex classes`

In order to create the equivalent Metadata (release) for each commit (here: starting from `v0:`),
run the following git rebase after you created your scenario.

```console
$ git rebase -i -X theirs --exec "rm -rf src && sfdx force:source:convert -d src && git add src && git commit --amend --no-edit" :/'v0:'
```

Then show all the Metadata changes since the first change (here: `v1:`)

```console
$ git diff --no-renames HEAD^{/v1:} src
```

Last but not least, add the expected incremental deployment to `config/deployments/expected`.
