# cldkctl
`cldkctl` is a command-line interface (CLI) for interacting with Cloudeka AI API.

## Prerequisites
Before installing `cldkctl`, ensure you have `yq` installed. `yq` is required for YAML processing.

### Install `yq`
#### On Linux
```sh
sudo wget https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -O /usr/local/bin/yq
sudo chmod +x /usr/local/bin/yq
```

#### On macOS (Using Homebrew)
```sh
brew install yq
```

#### On Windows (Using Chocolatey)
```sh
choco install yq
```

Verify installation:
```sh
yq --version
```

---

## Installation
You can download the latest `cldkctl` binary from the [GitHub Releases](https://github.com/lintasarta/cldkctl/releases/latest).

### Step 1: Download the Binary
Go to the **latest release page** and download the appropriate binary for your OS and architecture:

| OS         | Architecture | File Format |
|------------|-------------|-------------|
| macOS      | arm64       | `.tar.gz`   |
| macOS      | x86_64      | `.tar.gz`   |
| Linux      | arm64       | `.tar.gz`   |
| Linux      | i386        | `.tar.gz`   |
| Linux      | x86_64      | `.tar.gz`   |
| Windows    | arm64       | `.zip`      |
| Windows    | i386        | `.zip`      |
| Windows    | x86_64      | `.zip`      |

#### Example (Linux/macOS)
```sh
wget https://github.com/Lintasarta/ai-cldkctl/releases/download/v<VERSION>/cldkctl-<VERSION>_<OS>_<ARCH>.tar.gz
```

Or download and extract in one line:
```sh
curl -L https://github.com/Lintasarta/ai-cldkctl/releases/download/v<VERSION>/cldkctl-<VERSION>_<OS>_<ARCH>.tar.gz | tar xz
```

---

### Step 2: Extract and Install

#### On Linux & macOS
```sh
tar -xvzf cldkctl-<VERSION>-<OS>_<ARCH>.tar.gz
chmod +x cldkctl
sudo mv cldkctl /usr/local/bin/
```

#### On Windows
1. Extract the ZIP file.
2. Move `cldkctl.exe` to a directory in your `PATH` (e.g., `C:\Program Files\cldkctl\`).
3. Add this directory to the system `PATH` if necessary.

Verify installation:
```sh
cldkctl --version
```

---
## Authenticating with Cloudeka

Before using `cldkctl`, you must authenticate with your Cloudeka access token.

You can do this in two ways:

#### 1. Provide the token directly:
```sh
cldkctl auth your_cldkctl_token
```

#### 2. Use interactive prompt:
```sh
cldkctl auth
```
You'll be prompted to enter your Cloudeka access token:

```
❯ Enter your token: cldk_  ✡ required
```

---

### Available Commands
```sh
cldkctl is a command line interface to interact with Cloudeka service.

Usage:
  cldkctl [flags]
  cldkctl [command]

Available Commands:
  auth         Log in to the Cloudeka service using your token
  balance      View the balance for each project
  billing      View project billing details
  completion   Generate the autocompletion script for the specified shell
  help         Help about any command
  kubernetes   Manage Kubernetes resources
  logs         View and manage activity logs in the organizations cloud
  notebook     Manage Notebooks
  organization Manage organization details, members, and roles
  profile      View and manage your profile information
  project      View and manage your projects
  registry     Manage your container registry
  token        View and manage your Cloudeka authentication tokens
  vm           Manage virtual machines (VMs)
  voucher      Manage project vouchers and credit balances

Flags:
  -U, --base-url string            Base URL for API requests
  -N, --default-namespace string   Set a default namespace (default "default")
  -P, --default-project string     Set a default project ID to avoid repeated entries
  -R, --default-registry string    Set a default registry
      --editor string              Set a default editor (default "vim")
  -h, --help                       help for cldkctl
      --max-retries int            Maximum number of retries for HTTP requests (default 3)
  -O, --organization string        Set an organization
  -t, --toggle                     Help message for toggle
      --version                    Version information

Use "cldkctl [command] --help" for more information about a command.
```

---

## Updating `cldkctl`
To update to the latest version, download the new binary from [GitHub Releases](https://github.com/lintasarta/cldkctl/releases/latest) and follow the installation steps again.

For Linux/macOS, you can replace the existing binary:
```sh
sudo mv cldkctl /usr/local/bin/
```

---

## License
This project is licensed under the MIT License.

