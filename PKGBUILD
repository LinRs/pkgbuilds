# Maintainer:  VirtualTam <virtualtam@flibidi.net>
# Contributor: Eugene Yudin aka Infy <Eugene dot Yudin at gmail dot com>
pkgname=goldendict-qt5-git
pkgver=1.5.0.RC.550.g1df1b3d
pkgrel=2
pkgdesc="Feature-rich dictionary lookup program."
arch=('i686' 'x86_64')
url="http://goldendict.org/"
license=('GPL3')
depends=('ffmpeg' 'hunspell' 'libao' 'libeb' 'libvorbis' 'libxtst' 'lzo2'
         'qt5-base' 'qt5-tools' 'qt5-webkit' 'qt5-x11extras' 'zlib')
makedepends=('git')
conflicts=('goldendict' 'goldendict-svn' 'goldendict-git-opt')
provides=('goldendict')
replaces=('goldendict' 'goldendict-svn' 'goldendict-git-opt')
_gitname="goldendict"
source=(git://github.com/goldendict/goldendict.git#branch=qt4x5)
sha256sums=(SKIP)

pkgver() {
  cd ${_gitname}
  git describe --always | sed 's|-|.|g'
}

prepare() {
  cd ${_gitname}
  msg "Fixing flags"
  echo "QMAKE_CXXFLAGS_RELEASE = $CFLAGS" >> goldendict.pro
  echo "QMAKE_CFLAGS_RELEASE = $CXXFLAGS" >> goldendict.pro
}

build(){
  cd ${_gitname}
  PREFIX="/usr" qmake-qt5
  make
}

package() {
  cd ${_gitname}
  make INSTALL_ROOT="${pkgdir}" install
}
