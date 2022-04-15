# `pre-commit` hooks
This is a collection of hooks for [`pre-commit`](https://pre-commit.com).
View the full/raw list here: [.pre-commit-hooks.yaml](.pre-commit-hooks.yaml).

In general, these are `system` hooks so that you don't spend time installing
extra copies of tools that you've already set up in your development
dependencies and CI workflow.

Some of these may have some opinionated defaults, but you can override these
with the `args` option.

## Python/Poetry
Typically, you would add your development tools to pyproject.toml so that you
can use them from the console and your IDE, but then this means that you need
to keep those versions in sync with the ones installed by your pre-commit hooks.
This can lead to surprising behavior (different formatting between CLI and hook
invocation of a tool) and even errors (e.g., pre-commit pins the tool version,
but doesn't pin transient dependencies, whereas Poetry does, which can allow
failures [like this](https://github.com/psf/black/issues/2964) to suddenly
occur in your CI).

The following hooks run the tools via `poetry run` so that there is no conflict:

* `poetry-black`
* `poetry-flake8`
* `poetry-mypy`
* `poetry-pytest`

An alternative is to use something like [sync_with_poetry](https://github.com/floatingpurr/sync_with_poetry),
which is a pre-commit hook that updates the versions explicitly.

## Rust
* `cargo-clippy`
* `cargo-fmt`

## .NET
* `dotnet-format`
