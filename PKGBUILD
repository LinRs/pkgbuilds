# Maintainer: gborzi <gborzi@ieee.org>
# Contributor: mickele <mimocciola@yahoo.com>
pkgname=gmsh
pkgver=3.0.6
pkgrel=2
pkgdesc="An automatic 3D finite element mesh generator with pre and post-processing facilities."
arch=('i686' 'x86_64')
url="http://gmsh.info/"
license=('custom')
depends=('fltk' 'lapack' 'med' 'opencascade' 'cairo')
makedepends=('cmake' 'desktop-file-utils' 'sed' 'swig')
optdepends=('gmsh-docs: docs for gmsh'
            'python2: for onelab.py'
            'python: for onelab.py')
options=(!emptydirs)
source=("${url}src/${pkgname}-${pkgver}-source.tgz" gmsh.desktop gmsh.completion)
sha256sums=('9700bcc440d7a6b16a49cbfcdcdc31db33efe60e1f5113774316b6fa4186987b'
            '43a8ca33ac917ee7196fdae305ff2c8cb9ae1072569ee546c0ce8ff580c966ae'
            '11605e97636a56cf51e445e65019526ee253bd2e0553fb71ba6d94488dcd34ef')

build() {
   cd "${srcdir}/${pkgname}-${pkgver}-source"

   # Help links to local doc (package gmsh-docs)
   sed -e "s|http://gmsh.info/doc/texinfo/|file:///usr/share/doc/gmsh/gmsh.html|" \
       -i Fltk/graphicWindow.cpp
   sed -e "s|http://gmsh.info/doc/|file:///usr/share/licenses/gmsh/|" \
       -i Fltk/helpWindow.cpp

   mkdir -p build

   cd build

   cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DENABLE_BUILD_SHARED=ON \
      -DENABLE_PETSC=FALSE .. 

   make
}

package() {

   cd "${srcdir}/${pkgname}-${pkgver}-source/build"
   make DESTDIR=${pkgdir} install
   install -D -m644 "${pkgdir}/usr/bin/onelab.py" "${pkgdir}/usr/lib/python2.7/site-packages/onelab.py"
   install -D -m644 "${pkgdir}/usr/bin/onelab.py" "${pkgdir}/usr/lib/python3.6/site-packages/onelab.py"
   rm "${pkgdir}/usr/bin/onelab.py"

   install -d "${pkgdir}/usr/share/pixmaps/${pkgname}"
   install -m644 ../utils/icons/*.png "${pkgdir}/usr/share/pixmaps/${pkgname}"
   install -D -m644 ../utils/icons/solid_32x32.png "${pkgdir}/usr/share/icons/${pkgname}.png"

   desktop-file-install --dir="${pkgdir}/usr/share/applications" \
    	"${srcdir}/${pkgname}.desktop"

   install -D -m 644 "../LICENSE.txt" "${pkgdir}/usr/share/licenses/$pkgname/LICENSE.txt"
   install -D -m 644 "../CREDITS.txt" "${pkgdir}/usr/share/licenses/$pkgname/CREDITS.txt"
   install -D -m644 $srcdir/gmsh.completion $pkgdir/etc/bash_completion.d/gmsh

   rm -rf ${pkgdir}/usr/share/doc
}
