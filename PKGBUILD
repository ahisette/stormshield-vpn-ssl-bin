# Maintainer: Alex Hisette <alex.hisette at gmail dot com>
pkgname=stormshield-vpn-ssl-bin
pkgver=5.1.3
pkgrel=1
pkgdesc="Official Stormshield SSL VPN client"
arch=('x86_64')
url='https://vpn.stormshield.eu'
license=('custom:proprietary')
depends=(
  'fontconfig'
  'icu'
  'krb5'
  'libx11'
  'libxcursor'
  'libxi'
  'libxrandr'
  'openssl'
  'openvpn'
)
provides=("${pkgname%-bin}")
conflicts=("${pkgname%-bin}")
install=stormshield-vpn-ssl-bin.install
options=('!debug')
source=(
  "https://vpn.stormshield.eu/download/sslvpnclient-x64-${pkgver}.deb"
  "stormshield-vpn-ssl.service"
)
sha256sums=(
  '7c1def3ef66dadacf675fbbf1e67f774738909f82534c4a96acaac3f5318c641'
  'c16f8b52e8eb210f3dccd2f49aa41e925d4be561f71e23373439f7e7c9f568ed'
)

prepare() {
  cd "$srcdir"
  tar -xf data.tar.*
}

package() {
  cd "$srcdir"

  cp -r usr "${pkgdir}/"
  cp -r etc "${pkgdir}/"
  cp -r opt "${pkgdir}/"

  # Ensure binaries are executable
  chmod +x "${pkgdir}/opt/stormshield/sslvpnclient/Modules/ssl-vpn/Services/SSLVPNService"
  chmod +x "${pkgdir}/opt/stormshield/sslvpnclient/SSLVPNClient"
  chmod +x "${pkgdir}/usr/bin/sslvpnclient"
  chmod +x "${pkgdir}/usr/bin/sslvpn-cli"

  # Install systemd service and upstream compatibility alias
  mkdir -p "${pkgdir}/usr/lib/systemd/system/"
  install -Dm644 "${srcdir}/stormshield-vpn-ssl.service" "${pkgdir}/usr/lib/systemd/system/stormshield-vpn-ssl.service"
  ln -s stormshield-vpn-ssl.service "${pkgdir}/usr/lib/systemd/system/sslvpn-module.service"
}
