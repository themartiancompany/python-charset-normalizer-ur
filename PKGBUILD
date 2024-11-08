# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: lilydjwg <lilydjwg@gmail.com>
# Contributor: lilac <lilac@build.archlinuxcn.org>
# Contributor: Dimitris Kiziridis <ragouel@outlook.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_Pkg=charset_normalizer
_pkg=charset-normalizer
pkgname="${_py}-${_pkg}"
pkgver=3.3.2
pkgrel=2
pkgdesc='Encoding and language detection alternative to chardet'
arch=(
  any
)
_http="https://github.com"
_ns="Ousret"
url="${_http}/${_ns}/${_Pkg}"
license=(
  MIT
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)
source=(
  "git+${url}.git#tag=${pkgver}"
)
b2sums=(
  '005698ff0db98835326e055cb0097048998d2657b5998d09c1fbd81e0ab6c0551c5faf6c9934e3865dcd337cb2f86646acef37cd65187bf334b50c8328233c9b'
)

pkgver() {
  cd \
    "${_Pkg}"
  git \
    describe \
    --tags
}

build() {
  cd \
    "${_Pkg}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_Pkg}"
  # Override addopts as they invoke coverage testing
  pytest \
    --override-ini="addopts="
}

package() {
  local \
    site_packages
  site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_Pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Symlink license file
  install \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${site_packages}/${_Pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: ts=2 sw=2 et:
