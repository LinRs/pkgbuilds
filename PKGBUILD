# Maintainer: Lin Ruoshui <lin.ruohshoei+archlinux at gmail dot com>
# Contributor: hexchain <i at hexchain.org>
pkgname=hmcl
_pkgname=HMCL
pkgver=3.2.129
pkgrel=2
pkgdesc="Hello Minecraft! Launcher, a powerful Minecraft launcher."
arch=('x86_64')
license=('GPL3')
url="https://github.com/huanghongxun/HMCL"
depends=('java-openjfx>=8' 'java-environment>=8')
noextract=("$pkgname-$pkgver.jar")
source=("hmcl-launch-script"
	"${pkgname}-${pkgver}.jar::${url}/releases/download/v${pkgver}/${_pkgname}-${pkgver}.jar"
        "${pkgname}.desktop"
	"${pkgname}_icon::https://raw.githubusercontent.com/huanghongxun/HMCL/javafx/HMCL/src/main/resources/assets/img/craft_table.png")
sha256sums=('0300218f29af82e9b302a94b37a4c9a92aea26b960bfd1b2e16c0130ac61cfcf'
            '1e9b8f0882d52df1231cb34ce07e556c132f42d25759b6e0679c1e772e9ede3c'
            '5780cf70f1afec0eb3cd8fc43297d361903c7204e274a28c5edf9b8ac3eea83e'
            '2989a1b5301b8c7b9afdae5696c6a4e5246afa2d4f1f3d3dad5c192f036a9b4c')
package() {
    install -D -m755 "hmcl-launch-script" "${pkgdir}/usr/bin/$pkgname"
    install -D -m644 "$pkgname-${pkgver}.jar" "${pkgdir}/usr/share/$pkgname/HMCL.jar"
    install -D -m644 "hmcl.desktop" "${pkgdir}/usr/share/applications/hmcl.desktop"

    # install icon
    install -Dm644 "${pkgname}_icon" "$pkgdir/usr/share/icons/hicolor/48x48/apps/$pkgname.png"
}
