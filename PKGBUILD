# Maintainer: Xiao-Long Chen <chenxiaolong@cxl.epac.to>

pkgname=compizconfig-backend-gconf-ubuntu
_ubuntu_rel=0ubuntu5
pkgver=0.9.5.92.${_ubuntu_rel}
pkgrel=100
pkgdesc="GConf backend for Compiz - Ubuntu version"
url="http://www.compiz.org/"
license=('GPL' 'LGPL' 'MIT')
arch=('i686' 'x86_64')
depends=('gconf' 'libcompizconfig-ubuntu' 'glib2-ubuntu')
makedepends=('intltool' 'cmake' 'libtool' 'pkgconfig')
provides=('compizconfig-backend-gconf')
conflicts=('compizconfig-backend-gconf')
groups=('unity')
source=("https://launchpad.net/ubuntu/+archive/primary/+files/${pkgname%-*}_${pkgver%.*}.orig.tar.gz"
        "https://launchpad.net/ubuntu/+archive/primary/+files/${pkgname%-*}_${pkgver%.*}-${_ubuntu_rel}.debian.tar.gz")
sha512sums=('d03bd33ab21af915825a1f51dbc8411ce3edea5e485ce6f90a6f65cefeb3b1b949254ac93da655f1abb2ec4bc25010ba1c6858f62fa1a8510e05c0a938685f67'
            'd8c99a4b9b294cfd60875599f0f8811e8fbe59c26d6accb5e7b615aa24dec7065dac6371b07df65cec502f304c685cdd2dc033a0775ff03bee3272efbe8eec8e')

build() {
  cd "${pkgname%-*}-${pkgver%.*}"

  # Apply Ubuntu patches
  for i in $(cat "${srcdir}/debian/patches/series" | grep -v '#'); do
    patch -Np1 -i "${srcdir}/debian/patches/${i}"
  done

  [[ -d build ]] || mkdir build
  cd build
  cmake .. \
    -DCOMPIZ_BUILD_WITH_RPATH=FALSE \
    -DCOMPIZ_PACKAGING_ENABLED=TRUE \
    -DCOMPIZ_PLUGIN_INSTALL_TYPE=package \
    -DCMAKE_BUILD_TYPE=RelWithDebInfo \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCOMPIZ_DESTDIR="${pkgdir}"

  make ${MAKEFLAGS}
}

package() {
  cd "${srcdir}/${pkgname%-*}-${pkgver%.*}/build"
  make install
}

# vim:set ts=2 sw=2 et:
