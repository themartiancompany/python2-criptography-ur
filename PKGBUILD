# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  Pellegrino Prevete <cGVsbGVncmlub3ByZXZldGVAZ21haWwuY29tCg== | base -d>
# Maintainer:  Truocolo <truocolo@aol.com>
# Contributor: Felix Yan <felixonmars@archlinux.org>

_py=python
_pkg=cryptography
pkgname="${_py}-${_pkg}"
# Do NOT update. 3.4.0 dropped support for Python 2
pkgver=3.3.2
pkgrel=2
_pkgdesc=(
  "A package designed to expose cryptographic"
  "recipes and primitives to Python developers"
  "(Legacy Python 2 version)"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'arm'
  'armv6l'
  'armv7h'
  'aarch64'
  'i686'
  'pentium4'
  'x86_64'
  'mips'
  'powerpc'
)
license=(
  'Apache'
)
url="https://pypi.python.org/pypi/${_pkg}"
depends=(
  'python2-six'
  'python2-cffi'
  'python2-enum34'
  'python2-ipaddress'
  'glibc'
  'openssl-1.1'
  'python2'
)
makedepends=(
  'python2-setuptools'
)
checkdepends=(
  'python2-setuptools'
  'python2-pytest-runner'
  'python2-pretend'
  'python2-iso8601'
  'python2-pytz'
  'python2-hypothesis'
  "python2-cryptography-vectors=$pkgver"
)
optdepends=(
  'python2-bcrypt: for OpenSSH private key support'
)
source=(
  "https://pypi.io/packages/source/c/cryptography/cryptography-$pkgver.tar.gz"
)
sha512sums=(
  '55f6ee13342b3209b1fcb310f4c4d33d22856ee785cb2347e6ad36c34e9b42f6e0d5bece8e458b09663a5b78e34c4567fe7a211b51ca71f55ccc93e3f62dc5e4'
)

build() {
  cd \
    "${_pkg}-${pkgver}"

  # Explicitly build against OpenSSL 1.1.
  # Otherwise we end up building against the OpenSSL 3 headers
  # even though this version of cryptography
  # doesn't support OpenSSL 3, yet.
  CFLAGS+=" -I/usr/include/openssl-1.1"
  LDFLAGS+=" -L/usr/lib/openssl-1.1"
  "${_py}" \
    setup.py \
      build
}

check() {
  cd \
    cryptography-$pkgver
  python2 \
    setup.py \
      pytest
}

package() {
  cd \
    cryptography-$pkgver
  python2 \
    setup.py \
      install \
        --root="${pkgdir}" \
        --optimize=1 \
        --skip-build
}

# vim:set sw=2 sts=-1 et:
