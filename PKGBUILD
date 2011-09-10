# Maintainer: damir <damir@archlinux.org>

pkgname=ladspa
pkgver=1.13
pkgrel=3
pkgdesc="Linux Audio Developer's Simple Plugin API (LADSPA)"
arch=('i686' 'x86_64')
license=('LGPL')
url="http://www.ladspa.org/"
depends=('gcc-libs')
source=("http://www.ladspa.org/download/${pkgname}_sdk_${pkgver}.tgz"
        'hardcode-path.patch')
md5sums=('671be3e1021d0722cadc7fb27054628e'
         '27743258232d828575d66940e6de2858')

build() {
  cd "${srcdir}/${pkgname}_sdk/src"
  patch -Np1 -i "${srcdir}/hardcode-path.patch"
  sed \
    -e 's/mkdirhier/mkdir -p/' \
    -e "s#-O3#${CFLAGS} ${LDFLAGS/,--as-needed/}#" \
    -i makefile
  make targets
}

package() {
  cd "${srcdir}/${pkgname}_sdk/src"
  make INSTALL_PLUGINS_DIR="${pkgdir}/usr/lib/ladspa/" \
       INSTALL_INCLUDE_DIR="${pkgdir}/usr/include/" \
       INSTALL_BINARY_DIR="${pkgdir}/usr/bin/" install
}
