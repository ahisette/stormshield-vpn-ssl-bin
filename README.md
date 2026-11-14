# Stormshield SSL-VPN client for Arch Linux

[![Packaged version](https://img.shields.io/badge/dynamic/regex?url=https%3A%2F%2Fraw.githubusercontent.com%2Fahisette%2Fstormshield-vpn-ssl-bin%2Fmain%2F.SRCINFO&search=pkgver%20%3D%20(%5B0-9.%5D%2B)&replace=%241&label=version)](PKGBUILD)

This repository packages Stormshield's 64-bit Debian client for Arch Linux.

## Install

Building the package requires Arch Linux, `base-devel`, and `git`.

```bash
git clone https://github.com/ahisette/stormshield-vpn-ssl-bin.git
cd stormshield-vpn-ssl-bin
makepkg -si
```

## Service and usage

Enable the daemon, which also installs the `sslvpn-module.service` alias.

```bash
sudo systemctl enable --now stormshield-vpn-ssl.service
```

Launch the GUI with `sslvpnclient`, or run `sslvpn-cli --help` for the CLI. If the client cannot connect to the daemon, check `systemctl status stormshield-vpn-ssl.service` or read `journalctl -u stormshield-vpn-ssl.service -e`.

## License

Stormshield owns the VPN client software. The packaging scripts use the [MIT license](LICENSE).
