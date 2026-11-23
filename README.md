# Opinionated Python project starter with batteries included [![.github/workflows/ci.yaml](https://github.com/fcole90/python-poetry-starter/actions/workflows/ci.yaml/badge.svg)](https://github.com/fcole90/python-poetry-starter/actions/workflows/ci.yaml)

This project is designed to be a quick-start for Python projects, providing a set of tools and configurations that make development easier. It includes:

- Initial uv setup with local virtualenv and including poe task runner
- Test setup with pytest
- Linting setup with blake
- Typechecking setup with pyright
- Continuous integration with GitHub Actions

## Requirements

- macOS/Linux: `curl -LsSf https://astral.sh/uv/install.sh | sh`
or
- Windows: `powershell -c "irm https://astral.sh/uv/install.ps1 | iex"`

uv can manage Python versions directly. To install Python 3.13 via uv: `uv python install 3.13`

## Installation

```sh
uv sync
```

After this step you may want to close and reopen your terminal or IDE to ensure that the uv-managed virtual environment is activated correctly.

## Shared agent skills

This template consumes shared agent skills from [`swiftpostlabs/agentic-tools`](https://github.com/swiftpostlabs/agentic-tools). `.agents/config.json` lists them, and `.agents/agentic-tools.lock` pins the commit they come from.

After `uv sync`, link them into `.agents/skills/` with:

```sh
uv run poe sync-skills
```

The command exports the pinned commit into the gitignored `.agents/local/sources/` and links the skills from there, so `.agents/skills/` is generated locally rather than tracked in git. Move the pin to the latest skills with `uv run agentic-tools skills update`.

## Agent policy

This template also uses the installed `agentic-tools` package for policy sync instead of shipping a repo-local wrapper script.

Sync the generated agent policy files with:

```sh
uv run poe sync-ai-policy
```

Check policy drift without rewriting generated files with:

```sh
uv run poe policy-check
```

## Initialize a project

Run the initializer through uv so it uses the managed environment:

```sh
uv run poe init-project
```

You can also pass the name directly:

```sh
uv run poe init-project --name cool-app
```

The initializer validates the project name, renames `src/my_project` to the underscore form, and updates `pyproject.toml` accordingly.

## Tests

```sh
uv run poe test
```

## Linting

```sh
uv run poe lint
```

## Typechecking

```sh
uv run poe typecheck
```
