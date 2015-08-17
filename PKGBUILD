# Maintainer: OS Hazard <oshazard+aur@gmail.com>
# Contributor: Callan Barrett <wizzomafizzo@gmail.com>
# Contributor: Extraterrestrial <f564264@yandex.ru>

pkgname=w9wm-patched
pkgver=0.4.2
pkgrel=3
pkgdesc="w9wm with some small patches: alt+tab instead of ctrl+tab, reversed border colors, scrolling virtuals with mouse wheel, cursor from rio and sweeping any window instead of 9term only"
arch=('i686' 'x86_64')
url="http://www.grassouille.org/code/w9wm.en.html"
license=('custom')
depends=('libxext' 'libxau' 'libxdmcp' 'xterm')
makedepends=('imake' 'sed')
conflicts=('w9wm')
source=(http://www.grassouille.org/code/w9wm/src/w9wm-$pkgver.tar.gz
        rio-cursor.diff
        anywindow-sweep.diff
        scroll-virtuals.diff
        reverse-border-color.diff
        alttab.diff
        nograb.diff)
md5sums=('4c4bf243d9ae1478878c2b3bfcda144f'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

build() {
  cd $srcdir/w9wm-$pkgver.orig
  xmkmf
  make
}

package() {
  cd $srcdir/w9wm-$pkgver.orig/
  sed -i 's/MAXHIDDEN   32/MAXHIDDEN   128/' dat.h
  for i in "${srcdir}/*.diff"; do
      cat $i | patch -p0
  done
  mkdir -p $pkgdir/usr/bin
  make DESTDIR="${pkgdir}" install install.man
  chmod +x $pkgdir/usr/bin/w9wm
  install -Dm644 README.9wm ${pkgdir}/usr/share/licenses/w9wm/README.9wm
}
