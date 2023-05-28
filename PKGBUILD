# Maintainer: jmcb <joelsgp@protonmail.com>
# Contributor: ValHue <vhuelamo at gmail dot com>

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

    # Data
    install -d ${pkgdir}/opt/${pkgname}/{icons,lib,locales,pnacl,swiftshader}
    install -d ${pkgdir}/usr/share/{applications,licenses}
    install -m 644 icons/* "${pkgdir}/opt/${pkgname}/icons/"
    install -m 755 lib/* "${pkgdir}/opt/${pkgname}/lib/"
    install -m 644 locales/* "${pkgdir}/opt/${pkgname}/locales/"
    install -m 644 pnacl/* "${pkgdir}/opt/${pkgname}/pnacl/"
    install -m 644 swiftshader/* "${pkgdir}/opt/${pkgname}/swiftshader/"
    rm -rf ./{icons,lib,locales,pnacl,swiftshader}
    chmod +x ${pkgdir}/opt/${pkgname}/pnacl/*_nexe

    # Desktop file
    install -D -m 644 ${pkgname}.desktop "${pkgdir}/usr/share/applications/${pkgname}.desktop"

    # Rest of data
    install -m 644 ./* "${pkgdir}/opt/${pkgname}/"

    # Fix for permissions
    chmod +x ${pkgdir}/opt/${pkgname}/{chromedriver,launcher*,minidump_stackwalk,nacl_*,nwjc,payload,run}
}
