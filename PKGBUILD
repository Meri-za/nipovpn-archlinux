# Maintainer: <Meri-za@outlook.com>

pkgname='nipovpn'
pkgver='1.1.59'
pkgrel='1'
pkgdesc='A powerful proxy tool designed to conceal your HTTP requests within fake HTTP requests. This program, written in C++, leverages the Boost library to handle networking functionalities efficiently.'
arch=('x86_64')
# url='https://github.com/MortezaBashsiz/nipovpn' # Url Changed because the project repository was moved from AUR to GitHub.
url='https://github.com/Meri-za/nipovpn-archlinux'
license=('GPL3')
depends=('boost' 'boost-libs' 'yaml-cpp' 'glibc' 'openssl')
makedepends=('cmake' 'gcc' 'git')
options=('debug')

# Source Disabled because the project repository was moved from AUR to GitHub.
# source=("${pkgname}-${pkgver}.tar.gz::https://github.com/MortezaBashsiz/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
# sha256sums=('SKIP')

build() {
  cmake -B build -S .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_CXX_FLAGS="${CXXFLAGS}"
  cmake --build build --parallel "$(nproc)"
}

package() {
  # Install
  DESTDIR="$pkgdir" cmake --install build
  # Binary
  install -Dm755 build/core/nipovpn "${pkgdir}/usr/bin/${pkgname}"
  # Path
  cd "$srcdir/../$pkgname"
  # Services
  install -Dm644 usr/lib/systemd/system/nipovpn-agent.service "${pkgdir}/usr/lib/systemd/system/nipovpn-agent.service"
  install -Dm644 usr/lib/systemd/system/nipovpn-server.service "${pkgdir}/usr/lib/systemd/system/nipovpn-server.service" 
  # Config
  install -Dm644 etc/nipovpn/config.yaml "${pkgdir}/etc/${pkgname}/config.yaml"
  # Log
  install -Dm644 /dev/null "${pkgdir}/var/log/nipovpn/nipovpn.log"
}
