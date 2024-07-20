## Description
This is an opinionated base DevSpace file, with commonly used functions.

Refer to [REF.md](REF.md) for a list of available functions.

## Commands
- `devspace run reset` - deletes the namespace.

## devspace.yaml Structure & Logic
- `functions` - shared helpers for pipelines.
  - Each non-core function must define "$FUNCTION_NAME", "$FUNCTION_ARGS" and start with `function_init`. This does not 
    apply to `core` and `getter` functions.
- `pipelines` - where the logic happens.
  - Each non-core pipeline (i.e. dev, deploy) must define "$PIPELINE_NAME" and "$PIPELINE_FLAGS" and start with 
    `pipeline_init`.
- `commands` - essentially, wrappers for pipelines, meant to be used in dev environment only.
- The configuration enforces everything to run in the `${APP_NAME}` namespace. The value currently defaults to the repo 
  name, but can be overriden. Make sure to set all namespaces in your devspace.yaml file to `${APP_NAME}`.

Commands & pipelines naming conventions:
- Commands must be short, i.e. `<task-name>`, to make it easy to type.
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