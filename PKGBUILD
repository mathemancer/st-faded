# Maintainer:  blm  <blm@zedat.fu-berlin.de>

pkgname=st-faded
appname='st'
conflicts=(${appname})
provides=(${appname})
pkgver=0.8.1
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.  Patched with faded standard colors and scrollback'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(http://dl.suckless.org/st/$appname-$pkgver.tar.gz
            $pkgname-$pkgver.diff)
sha256sums=('SKIP'
            'SKIP')

prepare() {
  cd $srcdir/$appname-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/tic /d' Makefile
#  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$appname-$pkgver
  patch -i "$srcdir/$pkgname-$pkgver.diff"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$appname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
