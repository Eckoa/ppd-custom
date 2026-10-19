# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: tinywrkb <tinywrkb@gmail.com>

pkgname=ppd-custom
pkgname_=power-profiles-daemon
pkgver=0.30
pkgrel=1
pkgdesc='Makes power profiles handling available over D-Bus'
url='https://gitlab.freedesktop.org/upower/power-profiles-daemon'
license=(GPL-3.0-only)
arch=(x86_64)
depends=(glib2
         glibc
         libgcc
         libgudev
         polkit
         upower)
optdepends=('python-gobject: for powerprofilesctl')
makedepends=(bash-completion
             git
             glib2-devel
             python-argparse-manpage
             python-shtab
             meson)
checkdepends=(python-dbusmock
              python-isort
              python-mccabe
              umockdev)
provides=("$pkgname_")
conflicts=("$pkgname_" "power-profiles-daemon-git")
source=("git+https://gitlab.freedesktop.org/upower/$pkgname_#tag=$pkgver"
        "platform.patch"
        "pstate.patch")
sha256sums=('e955e833b01cbff9b5b00349592239e58c559d717eb49f3371f42932676e7a40'
            'a718dbbbf209cd1799ea9b987bc72997f4988c81f13c12c26447fe4de51d250d'
            '2dfb8fc94b121a91b6a9e549b2cc4df7c4a64b51e9da8ba68ba39da850772cdb')

prepare() {
  cd "$srcdir"
  patch -Np1 -i "$srcdir/platform.patch"
  patch -Np1 -i "$srcdir/pstate.patch"
}

build() {
  meson $pkgname_ build \
    --prefix /usr \
    --libexec lib \
    --sysconfdir /usr/share \
    -Dzshcomp=/usr/share/zsh/site-functions \
    -Dbashcomp=enabled \
    -Dmanpage=enabled
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}
