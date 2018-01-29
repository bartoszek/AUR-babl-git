# Maintainer: Alexander Hunziker <alex.hunziker@gmail.com>
# Contributor: Alessio Biancalana <dottorblaster@gmail.com>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: Salamandar <felix@piedallu.me>

pkgname=babl-git
_pkgname=babl
pkgver=0.1.42.2.g64c10d4
pkgrel=1
pkgdesc="babl is a dynamic, any to any, pixel format translation library."
arch=('i686' 'x86_64')
url="https://www.gegl.org/babl"
license=('LGPL3')
depends=('glibc')
makedepends=('git' 'meson')
provides=("babl=${pkgver}")
conflicts=('babl')
options=(!libtool)
source=(git://git.gnome.org/babl)
md5sums=('SKIP')

_gitname=babl

build() {
    mkdir "${srcdir}/build" -p

    meson "${srcdir}/${_gitname}"\
          "${srcdir}/build" \
        --prefix=/usr \
        -Dbuildtype=release \
        -Db_lto=true \
        -Dwith-docs=false

    ninja -C "${srcdir}/build"
}

package() {
    DESTDIR="${pkgdir}" ninja -C "${srcdir}/build" install
}

pkgver() {
    cd "${_gitname}"
    git describe --always | sed -e 's/BABL_//g' -e 's/[_-]/./g'
}

check() {
    meson test -C "${srcdir}/build"
}
