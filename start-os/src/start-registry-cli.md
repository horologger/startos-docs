# start-registry Reference

The `start-registry` CLI manages a StartOS package registry — the server that hosts, indexes, and distributes s9pk packages and OS updates. Run it on the registry server, or use `start-cli registry` to manage it remotely.

## Global Options

- `-c, --config <PATH>` — Configuration file path
- `-H, --host <URL>` — StartOS server URL
- `-r, --registry <URL>` — Registry URL
- `--registry-hostname <HOST>` — Registry server hostname
- `--s9pk-s3base <URL>` — Base URL for s9pk publishing
- `--s9pk-s3bucket <BUCKET>` — S3 bucket for publishing
- `-t, --tunnel <URL>` — Tunnel server address
- `-p, --proxy <URL>` — HTTP/SOCKS proxy
- `--cookie-path <PATH>` — Cookie file path
- `--developer-key-path <PATH>` — Developer signing key path

## Registry Info

### `start-registry index`

List registry metadata and all packages.

- `--format` — Output format

### `start-registry info`

Display the registry name and icon.

- `--format` — Output format

### `start-registry info set-name <NAME>`

Set the registry's display name.

### `start-registry info set-icon <ICON>`

Set the registry's icon from a file path.

## Admin Management

Manage registry administrators and their signing keys.

### `start-registry admin add <SIGNER> [DATABASE]`

Add a signer as an administrator.

### `start-registry admin remove <SIGNER>`

Remove an administrator.

### `start-registry admin list`

List all administrators.

- `--format` — Output format

### `start-registry admin signer add [DATABASE]`

Register a new signer identity.

- `-n, --name <NAME>` — Signer display name (required)
- `-c, --contact <INFO>` — Contact information
- `--key <KEY>` — Public key

### `start-registry admin signer edit <ID>`

Edit a signer's metadata.

- `-n, --set-name <NAME>` — Update name
- `-c, --add-contact <INFO>` — Add contact
- `-k, --add-key <KEY>` — Add public key
- `-C, --remove-contact <INFO>` — Remove contact
- `-K, --remove-key <KEY>` — Remove public key

### `start-registry admin signer list`

List all registered signers.

- `--format` — Output format

## Package Management

Add, remove, index, and distribute service packages.

### `start-registry package index`

List all packages and categories.

- `--format` — Output format

### `start-registry package add <FILE>`

Add a package to the registry from a local s9pk file.

- `--url <URL>` — URL of the package
- `--no-verify` — Skip signature verification

### `start-registry package remove <ID> <VERSION>`

Remove a package version from the registry.

- `--sighash <HASH>` — Hash for signature verification

### `start-registry package get [ID] [OTHER_VERSIONS]`

List installation candidates for a package.

- `-v, --target-version <RANGE>` — Version range constraint
- `--source-version <VERSION>` — Source version for upgrade path
- `--format` — Output format
- `OTHER_VERSIONS` — Detail level: `none`, `short`, or `full`

### `start-registry package download <ID>`

Download an s9pk package file.

- `-v, --target-version <RANGE>` — Version constraint
- `-d, --dest <PATH>` — Destination path

### `start-registry package add-mirror <FILE> <URL>`

Add a download mirror for a package.

- `--no-verify` — Skip signature verification

### `start-registry package remove-mirror <ID> <VERSION>`

Remove a package mirror.

- `--url <URL>` — Mirror URL to remove (required)

## Package Categories

Organize packages into browseable categories.

### `start-registry package category add <ID> <NAME>`

Create a new category.

### `start-registry package category remove <ID>`

Delete a category.

### `start-registry package category list`

List all categories.

- `--format` — Output format

### `start-registry package category add-package <ID> <PACKAGE>`

Add a package to a category.

### `start-registry package category remove-package <ID> <PACKAGE>`

Remove a package from a category.

## Package Signers

Manage cryptographic signers authorized for packages.

### `start-registry package signer add <ID> <SIGNER>`

Authorize a signer for a package.

- `--versions <RANGE>` — Version range to authorize
- `--merge` — Merge with existing range instead of replacing

### `start-registry package signer remove <ID> <SIGNER>`

Revoke a signer for a package.

### `start-registry package signer list <ID>`

List authorized signers for a package.

- `--format` — Output format

## OS Versions

Manage StartOS version records in the registry.

### `start-registry os index`

List all OS versions.

- `--format` — Output format

### `start-registry os version add <VERSION> <HEADLINE> <RELEASE_NOTES> <SOURCE_VERSION>`

Register a new OS version.

### `start-registry os version get`

Get OS version information with filters.

- `--src <VERSION>` — Source version to upgrade from
- `--target-version <VERSION>` — Target version constraint
- `--id <SERVER_ID>` — Server identifier
- `--platform <PLATFORM>` — Target platform
- `--format` — Output format

### `start-registry os version remove <VERSION>`

Remove an OS version.

### `start-registry os version signer add <VERSION> <SIGNER>`

Add a signer for an OS version.

### `start-registry os version signer remove <VERSION> <SIGNER>`

Remove a signer from an OS version.

### `start-registry os version signer list <VERSION>`

List signers for an OS version.

- `--format` — Output format

## OS Assets

Upload and manage OS installation images (IMG, ISO, squashfs).

### `start-registry os asset add <FILE> <URL>`

Upload an OS asset to the registry.

- `-p, --platform <PLATFORM>` — Target platform (required)
- `-v, --version <VERSION>` — OS version (required)

### `start-registry os asset sign <FILE>`

Sign an OS asset and register the signature.

- `-p, --platform <PLATFORM>` — Target platform (required)
- `-v, --version <VERSION>` — OS version (required)

### `start-registry os asset remove`

Remove an OS asset.

### `start-registry os asset get img <VERSION> <PLATFORM>`

Download an IMG file.

- `-d, --download <DIR>` — Download directory
- `-r, --reverify` — Verify hash after download

### `start-registry os asset get iso <VERSION> <PLATFORM>`

Download an ISO file. Same options as `get img`.

### `start-registry os asset get squashfs <VERSION> <PLATFORM>`

Download a squashfs file. Same options as `get img`.

## Database

Low-level access to the registry database.

### `start-registry db dump [-p <POINTER>] [PATH]`

Dump database contents, optionally filtered by JSON pointer.

- `-p, --pointer <PTR>` — JSON pointer
- `--format` — Output format

### `start-registry db apply <EXPR> [PATH]`

Apply a patch expression to the database.
