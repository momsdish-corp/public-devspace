# DevSpace Functions Reference

## Core Functions

### require_vars
Require variables to be set

**Parameters:**
- `$REQUIRE_VARS` - Array of variables to check

### function_init
Must be run at the beginning of every function that doesn't return a specific value

Example: `function_init my-function $@`

**Parameters:**
- `$COMMAND` - Name of the function
- `$ARGS` - (optional) All arguments passed to the function, i.e. $@)

### function_print
Print function messages

**Parameters:**
- `$MESSAGE` - Message to log

### pipeline_init
Must be run at the beginning of every pipeline
```bash
$PIPELINE_NAME my-pipeline
$PIPELINE_FLAGS="$(pipeline_print_flags flag1 flag2)"
pipeline_init
```

### pipeline_print
Log pipeline messages

**Parameters:**
- `$MESSAGE` - Message to show

### pipeline_print_flags
Print pipeline flags. Used by pipelines to declare the command.

Example: `pipeline_start my-pipeline $(pipeline_print_flags non-hidden-flag -hidden-flag)`

**Parameters:**
- `$FLAG_NAMES` - Array of flag names to print. If the flag name begins with a dash, the value will be hidden.

## Core Functions

### get_pod_by_label
Output the pod name or return error
RETURNS: pod name

**Parameters:**
- `$LABEL_VALUE` - Name of the label, i.e app.kubernetes.io/component=wordpress
- `$TIMEOUT` - (optional) (default: 1) timeout in seconds

## General Functions

### wait_for_pod_ready_or_debug
Wait for the pod to be ready. If not ready, it will output all logs and exit with an error.

**Parameters:**
- `$POD_NAME` - name of the pod to wait for
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds

### wait_for_pod_exec_or_debug
Wait for the pod to be ready for exec. If not ready, it will output all logs and exit with an error.

**Parameters:**
- `$POD_NAME` - name of the pod to wait for
- `$CONTAINER_NAME` - name of the container to wait for
- `$CONTAINER_TYPE` - (optional) (default: container) type of the container to wait for, i.e. initContainer, container
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds

### kubectl_follow_logs
Follow pod logs, until the pod finishes

**Parameters:**
- `$POD_NAME` - name of the pod to print logs for
- `$CONTAINER` - (optional) (default: all) name of the container to print logs for
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds

### kubectl_follow_logs_until_file_appears
Follow pod logs, until the specified file appears. The caveat is that the logs cannot start until the specified
container gets created.

**Parameters:**
- `$FILE_PATH` - absolute path of the file to wait for
- `$POD_NAME` - name of the pod to print logs for
- `$CONTAINER` - name of the container which holds the file
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds

### kubectl_list_pods
List all pods in the namespace

### kubectl_logs
Print logs for a pod

**Parameters:**
- `$POD_NAME` - name of the pod to print logs for
- `$CONTAINER` - name of the container to print logs for. If "all", it will print logs for all containers.

### kubectl_describe
Describe pod

**Parameters:**
- `$POD_NAME` - name of the pod to describe

### kubectl_status
Print status for a pod

**Parameters:**
- `$POD_NAME` - name of the pod to print status for

### kubectl_events
Print events for a pod

### validate_filename
Requires the string to start end with an alphanumeric character, may contain underscores, hyphens or dots, but not
repeating dots.

Example: `validate_filename "my-file-name"`

**Parameters:**
- `$FILENAME` - Filename to validate

### validate_namespace
Requires the string to start end with an alphanumeric character, and may contain hyphens.

Example: `validate_namespace "my-namespace"`

**Parameters:**
- `$STRING` - String to validate