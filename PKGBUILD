# Maintainer: jmcb <joelsgp@protonmail.com>
# Contributor: ValHue <vhuelamo at gmail dot com>

# todo change this to -bin, or change the pkgbuild to actually build it
pkgname='Snap4Arduino'
pkgver='8.2.4'
pkgrel=1
pkgdesc='A modification of the Snap! visual programming language that lets you seamlessly interact with almost all versions of the Arduino board.'
arch=('i686' 'x86_64')
url='http://snap4arduino.rocks/'
license=('AGPL3')
depends=('nss' 'libxtst' 'alsa-lib' 'libxss' 'gtk3' 'gconf' 'freetype2')
options=('!strip')

source=("$pkgname-$pkgver.patch")
source_i686=("https://github.com/bromagosa/${pkgname}/releases/download/${pkgver}/${pkgname}_desktop-gnu-32_${pkgver}.tar.gz")
source_x86_64=("https://github.com/bromagosa/${pkgname}/releases/download/${pkgver}/${pkgname}_desktop-gnu-64_${pkgver}.tar.gz")

sha256sums=('f7695f222543f4d9417d8871a206804a6bb27f93e5ae3ece1147778f9599f437')
sha256sums_i686=('f0779bc9ffd239e9c14ae51d711d9ed0c97b3c9afc3eff51e0a1b554a02338c0')
sha256sums_x86_64=('1d9fd14a56886898e4cbcb410a17c2fb5677e08a752ddd9939d0266dcad7a897')

if [[ $CARCH == 'i686' ]]; then
    _arch='32';
else
    _arch='64';
fi

prepare() {
    cd "${pkgname}_desktop-gnu-${_arch}_${pkgver}"
    patch -p1 -i "$srcdir/$pkgname-$pkgver.patch"
}

package() {
    cd "${pkgname}_desktop-gnu-${_arch}_${pkgver}"

    _opt="${pkgdir}/opt/${pkgname}"

    # Data directories
    install -D -m 644 -t "${_opt}/icons/" icons/*
    install -D -m 755 -t "${_opt}/lib/" lib/*
    install -D -m 644 -t "${_opt}/locales/" locales/*
    install -D -m 644 -t "${_opt}/pnacl/" pnacl/*

    # Desktop file
    install -D -m 644 -t "${pkgdir}/usr/share/applications/" "${pkgname}.desktop"

    # Rest of data
    find . -type 'f' -exec install -D -m 644 -t "${_opt}/" '{}' ';'

    # Fix for permissions
    chmod +x ${_opt}/pnacl/*_nexe
    chmod +x ${_opt}/{chrome_crashpad_handler,chromedriver,launcher.sh,minidump_stackwalk,nacl_*,nwjc,run}
}
