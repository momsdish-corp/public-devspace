# DevSpace Functions Reference

## wait_for_pod_ready_or_debug
Waits for the pod to be ready. If not ready, it will output all logs and exit with an error.

**Parameters:**
- `$POD_NAME` - name of the pod to wait for
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## wait_for_pod_exec_or_debug
Wait for the pod to be ready for exec. If not ready, it will output all logs and exit with an error.

**Parameters:**
- `$POD_NAME` - name of the pod to wait for
- `$CONTAINER_NAME` - name of the container to wait for
- `$CONTAINER_TYPE` - (optional) (default: container) type of the container to wait for, i.e. initContainer, container
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_follow_logs
Follow pod logs, until the pod finishes

**Parameters:**
- `$POD_NAME` - name of the pod to print logs for
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_follow_logs_until_file_appears
Follow pod logs, until the specified file appears. The caveat is that the logs cannot start until the specified 
container gets created.

**Parameters:**
- `$FILE_PATH` - absolute path of the file to wait for
- `$POD_NAME` - name of the pod to print logs for
- `$CONTAINER` - name of the container which holds the file
- `$TIMEOUT` - (optional) (default: 60) timeout in seconds
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_list_pods
List all pods in the namespace

**Parameters:**
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_logs
Print logs for a pod

**Parameters:**
- `$POD_NAME` - name of the pod to print logs for
- `$CONTAINER` - name of the container to print logs for. If "all", it will print logs for all containers.
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_describe
Describe pod

**Parameters:**
- `$POD_NAME` - name of the pod to describe
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_status
Print status for a pod

**Parameters:**
- `$POD_NAME` - name of the pod to print status for
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## kubectl_events
Print events for a pod

**Parameters:**
- `$REF_COMMAND` - (optional) Name of the referring command. This will be printed in the logs.

## get_pod_by_label
Output the pod name or return error

**Parameters:**
- `$LABEL_VALUE` - Name of the label, i.e app.kubernetes.io/component=wordpress
- `$TIMEOUT` - (optional) (default: 1) timeout in seconds

## require_vars
Require variables to be set

**Parameters:**
- `$REQUIRE_VARS` - Array of variables to check

## pipeline_start
Must be run at the beginning of every pipeline

**Parameters:**
- `$COMMAND` - Name of the command
- `$FLAGS` - (optional) Flags to pass to the command

## pipeline_end
Must be run at the end of every pipeline

**Parameters:**
- `$COMMAND` - Name of the command

## pipeline_print
Log pipeline messages

**Parameters:**
- `$COMMAND` - Name of the command
- `$MESSAGE` - Message to log

## pipeline_print_flags
Print pipeline flags. Used by pipelines to declare the command.

**Parameters:**
- `$FLAG_NAMES` - Array of flag names to print. If the flag name begins with a dash, the value will be hidden.

Example: `pipeline_start my-pipeline $(pipeline_print_flags non-hidden-flag -hidden-flag)`