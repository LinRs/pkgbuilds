# Maintainer: Lin Ruoshui <LinRs at yandex.com>
# Contributor: hexchain <i at hexchain.org>
pkgname=hmcl
pkgver=3.2.99
_pkgver=3.2.99
pkgrel=1
pkgdesc="Hello Minecraft! Launcher, a powerful Minecraft launcher."
arch=(any)
license=('GPL3')
url="https://github.com/mclauncher/HMCL"
makedepends=('unzip' 'imagemagick')
depends=('java-openjfx>=8' 'hicolor-icon-theme')
noextract=("HMCL-$pkgver.jar")
source=('hmcl-launch-script'
        'hmcl.desktop.in'
        # "$url/releases/download/v${pkgver%.*}/HMCL-$pkgver.jar")
	"HMCL-${_pkgver}.jar::https://github.com/huanghongxun/HMCL/releases/download/v${pkgver}/HMCL-${_pkgver}.jar"
	#"hmcl::git+$url.git#commit=cbb2a1b5755389b751d24730bc93de1011bed119"
	)

prepare() {
    cd "$srcdir"
    sed "s|@@VERSION@@|1.1|" hmcl.desktop.in > hmcl.desktop
    unzip -o "HMCL-$_pkgver.jar" assets/img/icon.png
}

#build() {
#    cd "$srcdir/hmcl"
#    chmod +x gradlew
#    ./gradlew clean build
#}

package() {
    cd "$srcdir"
    install -D -m755 "${srcdir}/hmcl-launch-script" "${pkgdir}/usr/bin/hmcl"
    install -D -m644 "${srcdir}/HMCL-${_pkgver}.jar" "${pkgdir}/usr/share/hmcl/HMCL.jar"
    install -D -m644 "${srcdir}/hmcl.desktop" "${pkgdir}/usr/share/applications/hmcl.desktop"

    # install icon
    cd "$srcdir/assets/img/"
    #install -Dm644 icon-new.png "$pkgdir/usr/share/icons/hicolor/32x32/apps/$pkgname.png"
     for size in 16 24 32 48 64 72 128 256 512; do
         target="$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/"
         mkdir -p $target
         convert icon.png -resize ${size}x${size} "$target/$pkgname.png"
     done
}
sha256sums=('0300218f29af82e9b302a94b37a4c9a92aea26b960bfd1b2e16c0130ac61cfcf'
            '648306b8b67fa9bcb531f065dabec20502ec8717788d1f65cf8e21b55c6c706c'
            'f341bc739ed24367a9a2d7572a0549103ac8c3ddf39ffc709f41f98817ed7c29')
