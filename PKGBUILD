# $Id$
# Maintainer: Piotr Gorski <lucjan.lucjanov@gmail.com>
# Contributor: Sergej Pupykin <arch+pub@sergej.pp.ru>

pkgname=psi-plus-git
pkgver=1.2.81.0.g79c7f8a
pkgrel=1
pkgdesc="Psi+ is a powerful Jabber client (Qt, C++) designed for the Jabber power users (built with Qt 5.x)"
url="http://psi-plus.com"
license=('GPL2')
arch=('i686' 'x86_64')
depends=('qt5-base' 'qt5-webkit' 'qt5-multimedia' 'qt5-x11extras' 'qca-qt5'
	 'libidn' 'aspell' 'libxss' 'qt5-svg')
makedepends=('git' 'patch' 'qconf-git')
provides=('psi-plus')
conflicts=('psi-plus-qt5-git' 'psi-plus-webkit-qt5-git' 'psi-plus-webkit-git' 'psi-plus')
source=("git://github.com/psi-plus/psi-plus-snapshots"
	"git://github.com/psi-plus/main.git"
	'conf.diff'
	'join.patch')
sha256sums=('SKIP'
            'SKIP'
            '690770c7c8976d536d8c4078d01c28f187f510574ddffe91251f5045fa672e53'
            '8b2ab645005fab4ca9c7fc84f57e94e1796309e780b535010b84eb0c191ad42c')


pkgver() {
  cd psi-plus-snapshots
  git describe --long --tags | sed 's/^v//;s/-/./g'
}            
            
prepare() {
  cd psi-plus-snapshots
  # make build date in --version output a bit more readable
  #sed "s/yyyyMMdd/yyyy-MM-dd/" -i qcm/conf.qcm
  mkdir -p iconsets
  cp -r "$srcdir"/main/iconsets/* ./iconsets
  echo "$pkgver ($(date +"%Y-%m-%d"))" >version
  patch -p1 <"$srcdir"/join.patch
}

build() {
  cd psi-plus-snapshots
  qconf
  patch -p0 < "$srcdir"/conf.diff
  ./configure --prefix=/usr \
              --libdir=/usr/lib \
              --disable-enchant \
              --enable-whiteboarding
  make
  patch -Rp0 < "$srcdir"/conf.diff
}

package() {
  cd psi-plus-snapshots

  make INSTALL_ROOT="$pkgdir" install

  install -dm755 "$pkgdir/usr/include/psi-plus/plugins"
  install -m644 src/plugins/include/*.h "$pkgdir/usr/include/psi-plus/plugins"
}
