# Maintainer: Lin Ruoshui <lin dot ruohshoei plus archlinux at gmail dot com>
# Contributor: hexchain <i at hexchain.org>
pkgname=hmcl
_pkgname=HMCL
pkgver=3.2.123
_pkgver=3.2.123
pkgrel=1
pkgdesc="Hello Minecraft! Launcher, a powerful Minecraft launcher."
arch=(any)
license=('GPL3')
url="https://github.com/huanghongxun/HMCL"
makedepends=('unzip' 'imagemagick')
depends=('java-openjfx>=8' 'hicolor-icon-theme')
noextract=("$pkgname-$pkgver.jar")
source=('hmcl-launch-script'
        'hmcl.desktop.in'
	"${pkgname}-${_pkgver}.jar::${url}/releases/download/v${pkgver}/${_pkgname}-${_pkgver}.jar"
	)

prepare() {
#    cd "$srcdir"
    sed "s|@@VERSION@@|1.1|" hmcl.desktop.in > hmcl.desktop
    unzip -o "$pkgname-$_pkgver.jar" assets/img/icon.png
}

package() {
#    cd "$srcdir"
    install -D -m755 "${srcdir}/hmcl-launch-script" "${pkgdir}/usr/bin/$pkgname"
    install -D -m644 "${srcdir}/$pkgname-${_pkgver}.jar" "${pkgdir}/usr/share/$pkgname/HMCL.jar"
    install -D -m644 "${srcdir}/hmcl.desktop" "${pkgdir}/usr/share/applications/hmcl.desktop"

    # install icon
#    cd "$srcdir/assets/img/"
    #install -Dm644 icon-new.png "$pkgdir/usr/share/icons/hicolor/32x32/apps/$pkgname.png"
    cd "assets/img/"
     for size in 16 24 32 48 64 72 128 256 512; do
         target="$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/"
         mkdir -p $target
         convert icon.png -resize ${size}x${size} "$target/$pkgname.png"
     done
}
sha256sums=('0300218f29af82e9b302a94b37a4c9a92aea26b960bfd1b2e16c0130ac61cfcf'
            '648306b8b67fa9bcb531f065dabec20502ec8717788d1f65cf8e21b55c6c706c'
            '85b1c41ba276513ddb6e4f6045f04a8eaa9de4a3cc93eff1fe795a00dba72615')
