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
	st-alpha-0.7.diff
        config.diff)
sha256sums=('f7870d906ccc988926eef2cc98950a99cc78725b685e934c422c03c1234e6000'
            'e89ef927e902f7bf679362ccfda3f03caca92540ebefaf56da24241993c5f30f'
            'SKIP')

prepare() {
  cp ${srcdir}/${_name}-${pkgver}/config.def.h .

  cd ${srcdir}/${_name}-${pkgver}

  msg2 "Applying alpha patch"
  patch -p1 < ../st-alpha-0.7.diff

  msg2 "Applying config patch"
  patch -p0 < ../config.diff
  
  # skip terminfo which conflicts with nsurses
  sed -i '/\@tic /d' Makefile
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
