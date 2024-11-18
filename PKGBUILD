# Maintainer: Grey Christoforo <first name [at] last name [dot] net>

pkgname=gpib-utils-git
_gitname=gpib-utils
pkgver=r254.720b17d
pkgrel=1
pkgdesc="GPIB instrument support utilities latest from master branch"
url="https://github.com/garlick/gpib-utils"
arch=('x86_64' 'i686')
license=('GPLv2')
depends=('linux-gpib' 'libtirpc')
source=("git+https://github.com/garlick/gpib-utils.git"
  0001-Fix-multiple-things-creating-warnings-also-remove-We.patch)
sha1sums=('SKIP'
  2c3073e15e725cf6a8685a1198d16a1d8473e51b)
provides=('gpib-utils')
conflicts=('gpib-utils')

pkgver() {
  cd "${srcdir}/$_gitname/"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${srcdir}/${_gitname}"
  patch -p1 <"../0001-Fix-multiple-things-creating-warnings-also-remove-We.patch"
  ./autogen.sh
  ./configure --prefix=${pkgdir}/usr CPPFLAGS="-I/usr/include/tirpc" LDFLAGS="-ltirpc"
}

build() {
  cd "${srcdir}/${_gitname}"
  make
}

package() {
  cd "${srcdir}/${_gitname}"
  make install
  mv ${pkgdir}/usr/etc ${pkgdir}/etc

  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim:set ts=2 sw=2 et:
