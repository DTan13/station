# Maintainer: Naoki Kanazawa <nk dot naoki912 at gmail dot com>
# Contributor: Yegorius <yegorius at domic dot us>
pkgname=station
pkgver=1.27.1
pkgrel=1
pkgdesc='The one app to rule them all'
arch=('x86_64')
url='https://getstation.com/'
license=('MIT')
#depends=('gtk2' 'gconf' 'xdg-utils' 'libxtst' 'libxss' 'nss' 'alsa-lib' 'xdg-utils')
source=(
    "https://github.com/getstation/desktop-app-releases/releases/download/${pkgver}/browserX-${pkgver}-x86_64.AppImage"
)
sha256sums=('674f3587348f5121221a7360e7338db9bd72277846ede289d3ec46c747033c75')

prepare() {
    chmod u+x ./browserX-${pkgver}-${arch}.AppImage
    ./browserX-${pkgver}-${arch}.AppImage --appimage-extract
}

package() {
    install -dm755 "${pkgdir}/usr/lib"
    install -dm755 "${pkgdir}/usr/share"
    install -dm755 "${pkgdir}/usr/bin"
    install -dm755 "${pkgdir}/usr/share/applications"

    cp -a "${srcdir}/squashfs-root" "${pkgdir}/usr/lib/${pkgname}"
    find "${pkgdir}/usr/lib/${pkgname}" -type d -exec chmod 755 "{}" \;

    cp -a "${srcdir}/squashfs-root/usr/share/icons" "${pkgdir}/usr/share"
    chmod -R 755 "${pkgdir}/usr/share/icons"

    sed -i -e 's/AppRun/station/' "${pkgdir}/usr/lib/${pkgname}/browserx.desktop"
    ln -s "/usr/lib/${pkgname}/browserx.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
    ln -s "/usr/lib/${pkgname}/browserx" "${pkgdir}/usr/bin/${pkgname}"
}