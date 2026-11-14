# Stormshield SSL-VPN Client for Arch Linux

This repository contains the PKGBUILD for the official Stormshield SSL-VPN client (`stormshield-vpn-ssl-bin`).
The package repackages the official 64-bit Debian binary package for Arch Linux.

## Requirements

You need the following items to build and run this package:

- An installation of Arch Linux or an Arch-based distribution
- The `base-devel` package group
- The `git` package

## Installation

Follow these steps to build and install the package:

1. Clone this repository:

   ```bash
   git clone https://github.com/ahisette/stormshield-vpn-ssl-bin.git
   ```

2. Go to the repository directory:

   ```bash
   cd stormshield-vpn-ssl-bin
   ```

3. Build and install the package:

   ```bash
   makepkg -si
   ```

## Upstream Update Checks

The [Check upstream version](.github/workflows/check-upstream-version.yml) workflow
checks the official Stormshield download page daily at 07:23 UTC. When a newer
upstream version is available, it downloads the Debian installer, computes its
SHA256, updates `PKGBUILD` and `.SRCINFO` on a `chore/pkg-update-<version>` branch,
and opens a pull request assigned to the repository owner. Existing pull requests
(including closed ones) prevent duplicate PRs.

You can also run it from **Actions > Check upstream version > Run workflow**.
The workflow must be published on the default branch, GitHub Actions must be
enabled, and **Allow GitHub Actions to create and approve pull requests** must be
enabled in **Settings > Actions > General**. It uses the automatic `GITHUB_TOKEN`;
no additional secret is needed.

Each run includes a version comparison in its summary. A download failure or an
unrecognized version makes the run fail rather than reporting the package as
up to date. If Stormshield changes its download page structure, the version
extraction may need updating.

## Service Configuration

The client requires a background daemon to manage VPN tunnels.

1. Enable and start the systemd service:

   ```bash
   sudo systemctl enable --now stormshield-vpn-ssl.service
   ```

2. Check the service status:

   ```bash
   systemctl status stormshield-vpn-ssl.service
   ```

> [!NOTE]
> The upstream service alias `sslvpn-module.service` also points to this service.

## Usage

### Graphical Interface

Start the graphical interface from your application menu or run the following command:

```bash
sslvpnclient
```

### Command-Line Interface

The package provides a command-line utility.
To display available options, run:

```bash
sslvpn-cli --help
```

## Troubleshooting

### Daemon Connection Failure

If the user interface cannot connect to the daemon, verify the service state:

```bash
systemctl status stormshield-vpn-ssl.service
```

If the service is inactive, restart the service:

```bash
sudo systemctl restart stormshield-vpn-ssl.service
```

### Log Files

To view system logs for the daemon, run:

```bash
journalctl -u stormshield-vpn-ssl.service -e
```

## License

The Stormshield SSL-VPN client is proprietary software provided by Stormshield.
The packaging scripts in this repository are available under the MIT license.
