# start-container Reference

The `start-container` CLI runs inside each service's LXC container and is used by the StartOS container runtime to manage service lifecycle, actions, and subcontainers. This is an internal system tool — it is **not** intended for end users.

> [!WARNING]
> These commands are called automatically by the StartOS container runtime and the SDK. Running them manually can corrupt service state, break running services, or cause data loss. They are documented here for package developers and system internals reference only. If you are a user looking to interact with a service container, use `start-cli package attach` instead — see [Accessing Service Containers](service-containers.md).

## Global Options

- `--socket <PATH>` — Path to the Unix socket for host communication

## Service Lifecycle

### `start-container get-status [PACKAGE_ID]`

Get the current status of a service.

### `start-container set-main-status <STATUS>`

Set the main status of the current service.

### `start-container restart`

Restart the container runtime.

### `start-container shutdown`

Shut down the container runtime.

### `start-container rebuild`

Rebuild the container environment.

## Actions

Run and manage service actions and tasks.

### `start-container action run <ACTION_ID> <INPUT>`

Execute a service action with the given input data.

- `-p, --package-id <ID>` — Package identifier
- `--format` — Output format

### `start-container action get-input <ACTION_ID>`

Get the input spec (form schema) for an action.

- `-p, --package-id <ID>` — Package identifier
- `--format` — Output format

### `start-container action clear`

Clear all registered actions.

- `--except <IDS>` — Action IDs to exclude from clearing

### `start-container action clear-tasks`

Clear pending tasks.

- `--only <IDS>` — Only clear these task IDs
- `--except <IDS>` — Task IDs to exclude

## Dependencies

### `start-container check-dependencies [PACKAGE_IDS...]`

Check whether service dependencies are satisfied.

### `start-container get-dependencies`

List the declared dependencies.

### `start-container set-dependencies [DEPENDENCIES]`

Update the dependency declarations.

## Data

### `start-container get-data-version`

Get the current data schema version.

### `start-container set-data-version [VERSION]`

Set the data schema version (used during migrations).

## Subcontainers

Manage subcontainers (process containers within the service's LXC container).

### `start-container subcontainer create-fs <IMAGE_ID> [NAME]`

Create a filesystem from a container image.

### `start-container subcontainer destroy-fs <GUID>`

Destroy a previously created filesystem.

### `start-container subcontainer exec <CHROOT> [COMMAND]`

Execute a command in an existing subcontainer filesystem.

- `--force-tty` — Force TTY mode
- `--force-stderr-tty` — Force stderr as TTY
- `--pty-size <ROWS:COLS>` — Terminal size
- `-e, --env <KEY=VALUE>` — Set environment variable
- `--env-file <PATH>` — Load env from file
- `-w, --workdir <PATH>` — Working directory
- `-u, --user <USER>` — Run as user

### `start-container subcontainer exec-command <CHROOT> [COMMAND]`

Execute a command in a subcontainer. Same options as `exec`.

### `start-container subcontainer launch <CHROOT> [COMMAND]`

Launch a long-running process in a subcontainer. Same options as `exec`.

### `start-container subcontainer launch-init <CHROOT> [COMMAND]`

Launch an init process in a subcontainer. Same options as `exec`.

## Utilities

### `start-container echo <MESSAGE>`

Echo a message back (connectivity test).

### `start-container get-os-ip`

Get the IP address of the host OS.

### `start-container git-info`

Display the build's git hash.

### `start-container plugin url`

Get the plugin URL for the container runtime.
