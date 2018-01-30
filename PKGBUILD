# Maintainer: Marco Pompili
# Contributor: Christoph Vigano <mail@cvigano.de>
# Contributor: Patrick Jackson <PatrickSJackson gmail com>

pkgname=st-br1
_name=st
pkgver=0.7
pkgrel=1
pkgdesc="A simple virtual terminal emulator for X."
url="http://st.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
makedepends=('ncurses')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
conflicts=('st')
provides=('st')
source=(http://dl.suckless.org/st/${_name}-${pkgver}.tar.gz
        config.h)
sha256sums=('f7870d906ccc988926eef2cc98950a99cc78725b685e934c422c03c1234e6000'
            '7bc5195bfcafac36f3c4f44b04e9934fb407714e9c9d871cd6ac1170bfb5cd7b')

prepare() {
  cd ${srcdir}/${_name}-${pkgver}
  # skip terminfo which conflicts with nsurses
  sed -i '/\@tic /d' Makefile
  cp ${srcdir}/config.h config.h
}

build() {
  cd ${srcdir}/${_name}-${pkgver}
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd ${srcdir}/${_name}-${pkgver}
  make PREFIX=/usr DESTDIR="${pkgdir}" TERMINFO="${pkgdir}/usr/share/terminfo" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README "${pkgdir}/usr/share/doc/${pkgname}/README"
}
