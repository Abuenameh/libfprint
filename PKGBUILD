pkgname=libfprint-sigfm-git
_pkgname=libfprint-sigfm
epoch=1
pkgver=1.94.5+sigfm
pkgrel=1
pkgdesc="Library for fingerprint readers"
url="https://fprint.freedesktop.org/"
arch=(x86_64)
license=(LGPL)
depends=(libgusb pixman nss systemd-libs opencv4 doctest)
makedepends=(git meson gtk-doc gobject-introspection systemd)
checkdepends=(python python-cairo python-gobject 'umockdev>=0.13.2')
provides=("libfprint=$pkgver" libfprint-2.so)
conflicts=(libfprint)
groups=(fprint)
source=("https://gitlab.freedesktop.org/0x00002a/libfprint/-/archive/sigfm/libfprint-sigfm.tar.bz2" "elan.patch")
sha256sums=('SKIP' 'SKIP')

prepare() {
  cd $_pkgname
  patch --forward --strip=1 --input="${srcdir}/elan.patch"
}

build() {
  arch-meson $_pkgname build
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  DESTDIR="$pkgdir" meson install -C build
}