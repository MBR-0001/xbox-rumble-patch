_pkgbase=xbox-rumble-patch
_kernel_tag=6.1-arch1
pkgname=${_pkgbase}-dkms
pkgver=1
pkgrel=1
pkgdesc='The xbox kernel module with a patch enabling rumble on newer xbox controllers'
license=('GPL')
arch=('i686' 'x86_64')
depends=('dkms')
optdepends=('linux-headers: Needed for build the module for Arch kernel'
            'linux-lts-headers: Needed for build the module for LTS Arch kernel'
            'linux-zen-headers: Needed for build the module for ZEN Arch kernel')
source=("hid-ids.h::https://raw.githubusercontent.com/archlinux/linux/v${_kernel_tag}/drivers/hid/hid-ids.h"
        "hid-microsoft.c::https://raw.githubusercontent.com/archlinux/linux/v${_kernel_tag}/drivers/hid/hid-microsoft.c"
        rumble-fix.patch
        Kbuild
        dkms.conf)
sha256sums=('03811ba8b9fdece29574d8ce7f07586daada604ee47f4b0e9a698aef40689b5d'
            'e33cc0e0cc6cd2744bf117ab1b23760f04f3275af20139c5c511315ca02ac04d'
            '45bba5f07e7866bceb874d211fdc4b8d2612183146b47e635906b63d0a13fcd0'
            'cd7a1473d1ee2dae2a28a130743389d6033c1503a84e8d4332fbc10631f067ed'
            '9dbde0a4544faa91eee8f9a2f2e639031b84ba0addd781af4740c3f55d4980ad')

prepare() {
    mkdir "${srcdir}/workdir"
    cd "${srcdir}/workdir"
    cp "${srcdir}/"{hid-ids.h,hid-microsoft.c} .
    patch -p3 <../rumble-fix.patch
}

package() {
    local dest="$pkgdir/usr/src/${_pkgbase}-$pkgver"
    mkdir -p $dest
    cd "${srcdir}/workdir/"
    cp --preserve=all {hid-ids.h,hid-microsoft.c} $dest
    cd "${srcdir}"
    cp --preserve=all Kbuild dkms.conf $dest
} 
