pkgname=(termite)
pkgver=99999.13.r25.gf7aa2d5
pkgrel=1

pkgdesc="A simple VTE-based terminal"
url="https://github.com/amosbird/termite/"
arch=('i686' 'x86_64')
license=('LGPL')

makedepends=('git' 'vte3' 'ncurses')

source=(git://github.com/amosbird/termite
        git+https://github.com/thestinger/util)

md5sums=(SKIP SKIP)

pkgver() {
  cd termite
  echo 99999.$(git describe --long --always | sed 's/^v//; s/-/.r/; s/-/./')
}

prepare() {
  cd termite
  git submodule init
  git config submodule.util.url "$srcdir"/util
  git submodule update
}

build() {
  cd termite
  make
}

package_termite() {
  pkgdesc="A simple VTE-based terminal"
  depends=('vte3')
  backup=(etc/xdg/termite/config)

  cd termite
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 config "$pkgdir"/etc/xdg/termite/config
  install -d "$pkgdir"/usr/share/terminfo
  tic -x termite.terminfo -o "$pkgdir"/usr/share/terminfo
}
