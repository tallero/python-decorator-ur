# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Thomas Dziedzic < gostrc at gmail >
# Contributor: Pierre Chapuis <catwell at archlinux dot us>

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
_pkg=decorator
pkgname="${_py}-${_pkg}"
pkgver=5.2.1
pkgrel=1
pkgdesc='Python Decorator module'
arch=(
  'any'
)
url="https://pypi.python.org/pypi/${_pkg}"
license=(
  'BSD-2-Clause'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
_pypa="https://pypi.python.org/packages/source"
source=(
  "${_pypa}/${_pkg:0:1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  'c834a3536e429aaff38d34a56b574344551c160e25676ca5febb5dcf521d71f284ebb8294d3264f65a801219860352377e5a4be89927217cb5da9cb6c6aa45ec'
)

build() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

package() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      "installer" \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  install \
    -Dm644 \
    "LICENSE.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

check() {
  cd \
    "$srcdir/${_pkg}-$pkgver"
  PYTHONPATH="src" \
  "${_py}" \
    -m \
      "unittest" \
    "discover" \
    -vs \
      "tests/"
}
