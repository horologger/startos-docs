# Accessing Service Containers

Every service on StartOS runs inside its own isolated LXC container. StartOS provides `start-cli package attach` to open a shell inside a service's container — this is the supported way to access containers. StartOS does not use Docker or Podman; standard container tooling will not work. See the [CLI Reference](cli-reference.md) for the full list of `start-cli` options.

> [!WARNING]
> Accessing a service container is an advanced operation. Modifying files, stopping processes, or changing configuration inside the container can break the service or cause data loss. Proceed with caution.

## Why Access a Service Container?

There are several reasons you might want a shell inside a running service container:

- **Debugging** — Inspect logs, running processes, or file state when a service is misbehaving.
- **Querying a database** — Run ad-hoc queries against a service's database (e.g., `sqlite3`, `psql`, `redis-cli`) that aren't exposed through the UI.
- **Running CLI tools** — Many services ship their own command-line utilities (e.g., `bitcoin-cli`, `lncli`) that can be invoked directly inside the container.
- **Inspecting configuration** — View the generated config files or environment variables a service is actually running with.
- **Advanced recovery** — In rare cases, manually repair data or state that cannot be fixed through the StartOS UI.

## Usage

First, [SSH](ssh.md) into your StartOS server. Then attach to a running service:

```bash
start-cli package attach <PACKAGE>
```

Replace `<PACKAGE>` with the package identifier (e.g., `bitcoind`, `lnd`). You can find package identifiers with:

```bash
start-cli package list
```

Once attached, you are dropped into a shell inside the service's container. Type `exit` or press `Ctrl+D` to return to the host.
