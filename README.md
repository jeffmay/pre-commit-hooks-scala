# pre-commit-hooks-scala

This project contains [`pre-commit`](https://pre-commit.com) hooks for Scala projects.

## Installation

You can add and of the following [hooks](#hooks) by adding a `.pre-commit-config.yaml` file to the base of your repo with:

<!-- TODO: Automatically update this with the latest version of this repo -->
```yaml
repos:
  - repo: https://github.com/jeffmay/pre-commit-hooks-scala
    rev: v0.0.1
    hooks:
      - id: scalafmt
```

## Hooks

### scalafmt

Installs and bootstraps an executable jar of [`scalafmt` using coursier](https://scalameta.org/scalafmt/docs/installation.html#coursier). By using this method of installation, `scalafmt` will automatically download the version of `scalafmt` that is specified in your `.scalafmt.conf` file and cache it locally.

Whenever you call `pre-commit run` (either via `git` hook or manually), it will run the formatter on all staged files from `git`. You can run it on all files by passing the `--all-files` argument.

#### GitHub Action

You can add this to a github workflow by adding a `.github/workflows/release.yaml` file:

```yaml
name: Format
on:
  pull_request:
    branches: ['**']

jobs:
  pre-commit:
    name: pre-commit
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v3
      - uses: coursier/setup-action@v1
      - uses: pre-commit/action@v3.0.0
        with:
          extra_args: --all-files
```

_NOTE: I've added the `--all-files` argument to the sample workflow since it doesn't take much longer to run in parallel to your other github checks and you will likely want to make sure that formatting changes are always applied to all files to make sure nobody is forced to make formatting changes in files they didn't edit._
