# cldkctl

`cldkctl` is a command-line interface (CLI) for interacting with Cloudeka by Lintasarta services.

## Prerequisites

Before installing `cldkctl`, ensure you have `yq` installed. `yq` is required for YAML processing.

### Install `yq`

#### On Linux
```sh
sudo wget https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -O /usr/local/bin/yq
sudo chmod +x /usr/local/bin/yq
```

#### On macOS (Homebrew)
```sh
brew install yq
```

#### On Windows (Chocolatey)
```sh
choco install yq
```

Verify:
```sh
yq --version
```

---

## Installation

### Homebrew (macOS & Linux)
```sh
brew tap Lintasarta/cldkctl https://github.com/Lintasarta/cldkctl.git
brew install cldkctl
```

### Snap (Linux)
```sh
sudo snap install cldkctl
```

### Manual (all platforms)

Download the latest binary from [GitHub Releases](https://github.com/lintasarta/cldkctl/releases/latest).

| OS      | Architecture | Format   |
|---------|-------------|----------|
| macOS   | arm64       | `.tar.gz` |
| macOS   | x86_64      | `.tar.gz` |
| Linux   | arm64       | `.tar.gz` |
| Linux   | i386        | `.tar.gz` |
| Linux   | x86_64      | `.tar.gz` |
| Windows | arm64       | `.zip`   |
| Windows | i386        | `.zip`   |
| Windows | x86_64      | `.zip`   |

**Linux/macOS:**
```sh
curl -L https://github.com/Lintasarta/cldkctl/releases/download/v<VERSION>/cldkctl-<VERSION>_<OS>_<ARCH>.tar.gz | tar xz
chmod +x cldkctl
sudo mv cldkctl /usr/local/bin/
```

**Windows:** Extract the ZIP and move `cldkctl.exe` to a directory in your `PATH`.

Verify:
```sh
cldkctl --version
```

---

## Quick Start

### 1. Authenticate
```sh
cldkctl auth <your-token>
```
Or use interactive mode:
```sh
cldkctl auth
```

### 2. List your organizations and projects
```sh
cldkctl organization list
cldkctl project list
```

### 3. Set defaults (recommended)
```sh
cldkctl <command> --default-project <project-id> --organization <org-id>
```

### 4. Create a flexi instance (interactive TUI)
```sh
cldkctl flexi instance create --interactive=true
```

---

## Global Flags

These flags work on any command and can be used to avoid repeating common values:

| Flag                       | Default | Description                                    |
|----------------------------|---------|------------------------------------------------|
| `-P, --default-project`    | `""`    | Default project ID                             |
| `-O, --organization`       | `""`    | Organization ID                                |
| `--max-retries`            | `3`     | Max retries for HTTP requests                  |
| `--http-timeout`           | `30`    | HTTP request timeout in seconds                |

> **Note:** Boolean flags such as `--interactive`, `--auto-confirm`, and `--enabled` are **string** flags and accept `true` or `false` as values (e.g. `--interactive=true`, `-i=true`). They do not support bare `-i` (without a value) syntax.

---

## Command Reference

### Compute — Flexi Instances

`cldkctl flexi instance`

| Command            | Description                                       |
|--------------------|---------------------------------------------------|
| `list`             | List all flexi instances                          |
| `detail [name]`    | Show instance details (accepts name or ID)        |
| `create`           | Create a new flexi instance                       |
| `delete [name]`    | Delete a flexi instance                           |
| `start [name]`     | Start a stopped instance                          |
| `stop [name]`      | Stop a running instance                           |
| `reboot [name]`    | Reboot an instance (soft/hard)                    |
| `rebuild [name]`   | Rebuild an instance (recreate OS, keep data)      |
| `resize [name]`    | Resize an instance (change flavor)                |
| `resize-root-disk` | Resize the root disk                              |
| `rename [name]`    | Rename an instance                                |
| `console [name]`   | Get console URL                                   |
| `attach-interface` | Attach a network interface                        |
| `detach-interface` | Detach a network interface                        |
| `add-floatingip`   | Add a floating IP                                 |
| `ssh`              | Manage SSH public keys (list/add/delete)          |
| `create-cluster`   | Create an instance cluster                        |

> Most `--*-id` flags accept names as alternatives to UUIDs (e.g. `--vpc-id my-vpc`, `--flavor-id "2vCPU-4GB"`).

### Compute — Claw (GoClaw) Instances

`cldkctl claw instance`

| Command            | Description                         |
|--------------------|-------------------------------------|
| `list`             | List all claw instances             |
| `detail [name]`    | Show instance details               |
| `create`           | Create a new claw instance          |
| `delete [name]`    | Delete a claw instance              |
| `preview [name]`   | Preview instance configuration      |
| `ssh-key [name]`   | Get SSH key                         |
| `api-key [name]`   | Get API key                         |
| `provider`         | Manage LLM providers                |
| `agent`            | Manage agents                       |
| `channel`          | Manage communication channels       |
| `skill`            | Manage skills (upload/list/update)  |

### Flexi Networking

`cldkctl flexi network`

| Subcommand   | Commands                           |
|-------------|------------------------------------|
| `vpc`       | `list`, `create`, `detail`, `update`, `delete` |
| `subnet`    | `list`, `create`, `detail`, `update`, `delete` |
| `port`      | `list`, `create`, `detail`, `update`, `delete` |
| `floatingip`| `list`, `create`, `delete`, `unassign`, `reassign` |

> VPC, subnet, port, and floating IP flags accept names in addition to UUIDs.

### Flexi Storage

`cldkctl flexi storage`

| Command                     | Description                        |
|-----------------------------|------------------------------------|
| `list`                      | List storage volumes               |
| `create`                    | Create a new storage volume        |
| `detail [id-or-name]`       | Show volume details                |
| `delete [id-or-name]`       | Delete a storage volume            |
| `attach [id-or-name]`       | Attach to a compute instance       |
| `detach [id-or-name]`       | Detach from a compute instance     |
| `resize [id-or-name]`       | Resize a storage volume            |
| `sync [id-or-name]`         | Sync a storage volume              |

### Flexi Image

`cldkctl flexi image`

| Command                    | Description                          |
|----------------------------|--------------------------------------|
| `list`                     | List images                          |
| `available`                | List available OS images             |
| `detail [id-or-name]`      | Show image details                   |
| `delete [id-or-name]`      | Delete an image                      |
| `snapshot-vm`              | Snapshot a VM as an image            |
| `snapshot-storage`         | Snapshot storage as an image         |
| `snapshot-restore`         | Restore a snapshot                   |
| `custom-image`             | Create a custom image                |
| `backup-scheduler`         | Create a backup scheduler            |
| `backup-scheduler-list`    | List backup schedulers               |
| `backup-scheduler-delete`  | Delete a backup scheduler            |
| `backup-list`              | List backups                         |

### Flexi Security Groups

`cldkctl flexi security`

| Command                     | Description                        |
|-----------------------------|------------------------------------|
| `list`                      | List security groups               |
| `create`                    | Create a security group            |
| `update [id-or-name]`       | Update a security group            |
| `delete [id-or-name]`       | Delete a security group            |

### Flexi Reference Commands

| Command              | Description                    |
|----------------------|--------------------------------|
| `flexi flavor list`  | List instance flavors/sizes    |
| `flexi disk-type list` | List disk types               |
| `flexi disk-type list-size` | List disk size packages  |
| `flexi region list`  | List available regions         |
| `flexi region zone-list` | List availability zones    |
| `zone list`          | List zones (top-level)         |

---

## Other Services

| Command           | Description                              |
|-------------------|------------------------------------------|
| `balance`         | View balance per project                 |
| `billing`         | View project billing details             |
| `box`             | Object storage (Dekabox) — list/create/detail |
| `dns`             | DNS record management                    |
| `ssl`             | SSL certificate management               |
| `vpn`             | VPN management (IPsec/OpenVPN)           |
| `vm`              | Virtual machines (KubeVirt)              |
| `llm`             | Large language model service             |
| `baremetal`       | Bare metal server management             |
| `guard`           | Project guard policies                   |
| `ticket`          | Support ticket management                |
| `backup-vm`       | VM backup management                     |
| `vcluster`        | Virtual cluster management               |
| `registry`        | Container registry (list/create/quota/helm) |
| `notebook`        | Jupyter Notebook management              |
| `kubernetes`      | Kubernetes resource management           |
| `voucher-credit`  | Voucher credits (list/create/delete)     |
| `voucher-trial`   | Trial vouchers (list/create/claim)       |
| `token`           | Manage Cloudeka authentication tokens    |
| `auditlog`        | Activity logs                            |
| `completion`      | Generate shell autocompletion            |

---

## Updating

Download the latest binary from [GitHub Releases](https://github.com/lintasarta/cldkctl/releases/latest) and replace the existing binary:

```sh
sudo mv cldkctl /usr/local/bin/
```

---

## License

MIT License
