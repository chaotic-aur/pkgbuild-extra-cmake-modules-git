# Merged with official ABS extra-cmake-modules PKGBUILD by João, 2021/06/03 (all respective contributors apply herein)
# Maintainer: João Figueiredo & chaotic-aur <islandc0der@chaotic.cx>
# Contributor: FadeMind <fademind@gmail.com>
# Contributor: Alexey D. <lq07829icatm@rambler.ru>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules-git
pkgver=5.87.0_r3368.gdc86450
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=($CARCH)
url='https://community.kde.org/Frameworks'
license=(LGPL)
depends=(cmake)
makedepends=(git python-sphinx python-requests qt5-tools)
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
optdepends=('python-pyxdg: to generate fastlane metadata for Android apps'
            'python-requests: to generate fastlane metadata for Android apps'
            'python-yaml: to generate fastlane metadata for Android apps')
groups=(kf5-git)
source=("git+https://github.com/KDE/${pkgname%-git}.git"
        "ECM-no-init.py.patch"
        "Py2-no-sip.patch")
sha256sums=('SKIP'
            '5695e45c7621a00c0bca28f058c13b5d524f963a00b53337c8cefcdaf22c4b52'
            '23d7ab5223c0fc9586cea687f1b6f3928b67d6a937865ed1fbdbed1e02069218')

pkgver() {
  cd ${pkgname%-git}
  _ver="$(grep -m1 'set(VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
  echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

prepare() {
  patch -d ${pkgname%-git} -p1 < ECM-no-init.py.patch # Don't create __init__.py
  patch -d ${pkgname%-git} -p1 < Py2-no-sip.patch # Don't use python2 with sip
}

build() {
  cmake -B build -S ${pkgname%-git} \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DBUILD_HTML_DOCS=ON \
    -DBUILD_QTHELP_DOCS=ON
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
