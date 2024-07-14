## Description
This is an opinionated base devspace.yaml configuration commonly used functions.

## Commands
- `devspace run reset` - deletes the namespace.


## Structure
- `functions` - shared helpers for pipelines.
- `pipelines` - where the logic happens.
- `commands` - essentially, wrappers for pipelines, meant to be used in dev environment only.
- The app must be ran in the same namespace, defined in `${APP_NAME}` variable. Currently defaults to the repo name.
  Make sure to set all namespaces to `${APP_NAME}`.

Naming conventions:
- Commands must be short, i.e. `<task-name>`, to make it easy to type in.
- Most of the pipelines should be prefixed with "run-", i.e. `run-<task name>`.
- For example, a command `dump-db` would run a pipeline `run-dump-db`.

Pipeline structure:
- Must start with `pipeline_start <pipeline-name>`. This enforces the namespace, and helps debugging.
- Must echo with `pipeline_print <pipeline-name> <message>`.
- Must end with `pipeline_end <pipeline-name>`.

Restrictions:
- Commands must be restricted to dev environment. When adding new commands, make sure to restrict it.

## Usage
Here's how to import the base.yaml file into your project.

Paste the following code into your devspace.yaml file:

```
imports:
  - git: https://github.com/momsdish-corp/public-devspace.git
    branch: main
    subPath: base.yaml

```

For more information, refer to the [Devspace Docs](https://www.devspace.sh/docs/configuration/imports/)