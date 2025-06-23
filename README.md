andrewaylett/pre-commit-action
==============================

a GitHub action to run [pre-commit](https://pre-commit.com)

### using this action

To use this action, make a file `.github/workflows/pre-commit.yml`.  Here's a
template to get started:

```yaml
name: pre-commit

on:
  pull_request:
  push:
    branches: [main]

jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - uses: andrewaylett/pre-commit-action@v0
```

This does a few things:

- clones the code
- sets up the `pre-commit` cache

### using this action with custom invocations

By default, this action runs all the hooks against all the files.  `extra_args`
lets users specify a single hook id and/or options to pass to `pre-commit run`.

Here's a sample step configuration that only runs the `flake8` hook against all
the files (use the template above except for the `pre-commit` action):

```yaml
    - uses: andrewaylett/pre-commit-action@v0
      with:
        extra_args: flake8 --all-files
```

## History

This repository is forked from pre-commit/action, which was maintained by the
authors of pre-commit until they started their own CI service.

Having not found https://pre-commit.ci to be suitable for my use-cases, I have
continued to use the out-of-support GitHub Action.  It still works, but the
warnings (and outdated dependencies) make me prefer to maintain my own fork.
