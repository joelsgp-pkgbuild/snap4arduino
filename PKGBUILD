# Maintainer: jmcb <joelsgp@protonmail.com>
# Contributor: ValHue <vhuelamo at gmail dot com>

# todo change this to -bin, or change the pkgbuild to actually build it
pkgname='Snap4Arduino'
pkgver='6.2'
pkgrel=2
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
sha256sums_i686=('72bdf9138e26d29ba2c965eecd017c7235904414352e235323fa24374419d4b2')
sha256sums_x86_64=('312fd6a8aabfbe8d44a3f2795a0f93c2ed3da481b688150f3f54b78fdd9ecc3a')

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
    echo "${_opt}/icons/"
    install -D -m 644 -t "${_opt}/icons/" icons/*
    install -D -m 755 -t "${_opt}/lib/" lib/*
    install -D -m 644 -t "${_opt}/locales/" locales/*
    install -D -m 644 -t "${_opt}/pnacl/" pnacl/*
    install -D -m 755 -t "${_opt}/swiftshader/" swiftshader/* 

    # Desktop file
    install -D -m 644 -t "${pkgdir}/usr/share/applications/" "${pkgname}.desktop"

    # Rest of data
    find . -type 'f' -exec install -D -m 644 -t "${_opt}/" '{}' ';'

    # Fix for permissions
    chmod +x ${_opt}/pnacl/*_nexe
    chmod +x ${_opt}/{chromedriver,launcher*,minidump_stackwalk,nacl_*,nwjc,payload,run}
}
