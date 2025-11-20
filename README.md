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
    - uses: actions/checkout@93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5
    - uses: andrewaylett/pre-commit-action@89f5816efbcdd63c8e50cc588d57aaf595ac8c75 # v4
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
    - uses: andrewaylett/pre-commit-action@89f5816efbcdd63c8e50cc588d57aaf595ac8c75 # v4
      with:
        extra_args: flake8 --all-files
```

Note that the `--all-files` flag is specified as a default extra argument,
and needs to be re-added if the default is overridden.

## History

This repository is forked from pre-commit/action, which was maintained by the
authors of pre-commit until they started their own CI service.

Having not found https://pre-commit.ci to be suitable for my use-cases, I have
continued to use the out-of-support GitHub Action.  It still works, but the
warnings (and outdated dependencies) make me prefer to maintain my own fork.

## Maintenance

Renovate will bump versions of tools that this project depends on.
Once that's working properly, it includes bumping the default pre-commit version in actions.yaml.
The main GitHub actions workflow tags each commit to `main` with the version of pre-commit that's in use
and a counter to keep track of releases of that version number.

I recommend consumers use [Mend Renovate](https://www.mend.io/mend-renovate/) or similar to pin to specific commits,
but the Actions workflow will maintain a major version tag that you may use if you prefer.
