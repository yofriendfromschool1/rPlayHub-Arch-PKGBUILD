# Maintainer: yofriendfromschool1
pkgname=rplayhub-bin
pkgver=0.1.3
pkgrel=1
pkgdesc="iPhone Mirroring for Linux (binary repackage from official .deb)"
arch=('x86_64')
url="https://github.com/rPlayAI/rPlayHub"
license=('custom')
depends=('sdl2' 'openssl' 'zlib' 'curl' 'usbmuxd' 'mesa' 'libx11' 'libxext')
makedepends=('debtap')
source=("${pkgname}-${pkgver}.deb::https://github.com/rPlayAI/rPlayHub/releases/download/linux-v0.1.3/rplayhub_0.1.3-1_amd64.deb")
sha256sums=('SKIP')

package() {
    # Extract the .deb directly into $pkgdir
    # The .deb structure is: debian-binary, control.tar.*, data.tar.*
    # We only need data.tar.*, which contains the actual files.
    bsdtar -xf "$srcdir/${pkgname}-${pkgver}.deb" -C "$pkgdir" --strip-components=0 data.tar.*
    
    # The above extracts data.tar.* into $pkgdir, but we need to extract
    # the contents of data.tar.* itself.
    # Find the extracted data.tar file (it may have .xz, .gz, or .zst extension)
    local data_tar=$(find "$pkgdir" -maxdepth 1 -name 'data.tar.*' -type f | head -n1)
    if [ -z "$data_tar" ]; then
        error "data.tar not found in .deb"
    fi
    
    # Extract the actual filesystem contents
    bsdtar -xf "$data_tar" -C "$pkgdir"
    
    # Remove the temporary data.tar.* file
    rm -f "$data_tar"
}
