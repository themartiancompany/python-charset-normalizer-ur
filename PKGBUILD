# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>
# Contributor: lilac <lilac@build.archlinuxcn.org>
# Contributor: Dimitris Kiziridis <ragouel@outlook.com>

pkgname=python-charset-normalizer
pkgver=3.3.2
pkgrel=1
pkgdesc='Encoding and language detection alternative to chardet'
arch=(any)
url=https://github.com/Ousret/charset_normalizer
license=(MIT)
depends=(python)
makedepends=(
  git
  python-setuptools
)
checkdepends=(
  python-pytest
  python-pytest-cov
)
source=("git+$url.git#tag=$pkgver")
b2sums=('005698ff0db98835326e055cb0097048998d2657b5998d09c1fbd81e0ab6c0551c5faf6c9934e3865dcd337cb2f86646acef37cd65187bf334b50c8328233c9b')

pkgver() {
  cd charset_normalizer
  git describe --tags
}

build() {
  cd charset_normalizer
  python setup.py build
}

check() {
  cd charset_normalizer
  pytest
}

package() {
  cd charset_normalizer
  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
  install -Dm 644 LICENSE -t "$pkgdir"/usr/share/licenses/python-charset-normalizer/
}

# vim: ts=2 sw=2 et:
