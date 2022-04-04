#!/usr/bin/env bash

pkgname=vscode-insiders
pkgver=$(awk -F '[-.]' '{ print $7 }' <<<$(curl -ILs -o /dev/null -w %{url_effective} https://update.code.visualstudio.com/latest/linux-x64/insider))
pkgrel=1
pkgdesc="Editor for building and debugging modern web and cloud applications (insiders version)"
arch=('x86_64')
url="https://code.visualstudio.com/"
license=('custom: commercial')
depends=(libxkbfile gnupg gtk3 libsecret nss gcc-libs libnotify libxss glibc lsof)
optdepends=('glib2: Needed for move to trash functionality' 'libdbusmenu-glib: Needed for KDE global menu')
source_i686=(code_ia32_${pkgver}.tar.gz::https://update.code.visualstudio.com/latest/linux-ia32/insider)
source_x86_64=(code_x64_${pkgver}.tar.gz::https://update.code.visualstudio.com/latest/linux-x64/insider)
source_aarch64=(code_arm64_${pkgver}.tar.gz::https://update.code.visualstudio.com/latest/linux-arm64/insider)
source_armv7h=(code_armhf_${pkgver}.tar.gz::https://update.code.visualstudio.com/latest/linux-armhf/insider)
sha256sums_i686=('SKIP')
sha256sums_x86_64=('SKIP')
sha256sums_aarch64=('SKIP')
sha256sums_armv7h=('SKIP')

package() {
    if [ "${CARCH}" = "aarch64" ]; then
        _pkg=VSCode-linux-arm64
    elif [ "${CARCH}" = "armv7h" ]; then
        _pkg=VSCode-linux-armhf
    elif [ "${CARCH}" = "i686" ]; then
        _pkg=VSCode-linux-ia32
    else
        _pkg=VSCode-linux-x64
    fi

    install -d "${pkgdir}/usr/share/licenses/${pkgname}"
    install -d "${pkgdir}/opt/${pkgname}"
    install -d "${pkgdir}/usr/bin"
    install -d "${pkgdir}/usr/share/applications"
    install -d "${pkgdir}/usr/share/icons"
    install -d "${pkgdir}/usr/share/mime/packages"

    install -m644 "${srcdir}/${_pkg}/resources/app/LICENSE.rtf" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.rtf"
    install -m644 "${srcdir}/${_pkg}/resources/app/resources/linux/code.png" "${pkgdir}/usr/share/icons/${pkgname}.png"
    install -Dm 644 "${srcdir}/${_pkg}/resources/completions/bash/code-insiders" "${pkgdir}/usr/share/bash-completion/completions/code-insiders"
    install -Dm 644 "${srcdir}/${_pkg}/resources/completions/zsh/_code-insiders" "${pkgdir}/usr/share/zsh/site-functions/_code-insiders"

    install -m644 "${startdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
    install -m644 "${startdir}/${pkgname}-url-handler.desktop" "${pkgdir}/usr/share/applications/${pkgname}-url-handler.desktop"
    install -m644 "${startdir}/${pkgname}-workspace.xml" "${pkgdir}/usr/share/mime/packages/${pkgname}-workspace.xml"

    cp -r "${srcdir}/${_pkg}/"* "${pkgdir}/opt/${pkgname}" -R
    ln -s "/opt/${pkgname}/bin/code-insiders" "${pkgdir}/usr/bin/code-insiders"
}
