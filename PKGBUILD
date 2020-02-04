# Maintainer: Jonathan Schilling (jonathan.schilling@mail.de)
pkgname=grpc-git
pkgver=1.26.0
pkgrel=5
pkgdesc="grpc"
arch=('x86_64')
url="https://github.com/grpc/grpc"
license=('Apache')
depends=(protobuf c-ares-cmake openssl)
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=()
md5sums=()

prepare() {
  git clone --depth 1 --recursive -b v${pkgver} https://github.com/grpc/grpc.git
  cd "$srcdir/${pkgname%-git}"
  git apply ../../patch_TraceFlagList.patch
  mkdir -p cmake/build
}

build() {
  cd "$srcdir/${pkgname%-git}/cmake/build"
  cmake \
    -DBUILD_SHARED_LIBS=ON \
    -DgRPC_CARES_PROVIDER="package" \
    -DgRPC_PROTOBUF_PROVIDER="package" \
    -DgRPC_SSL_PROVIDER="package" \
    -DgRPC_ZLIB_PROVIDER="package" \
    -DCMAKE_INSTALL_PREFIX="$pkgdir/usr" \
    ../..
  make -j 8
}

package() {
  cd "$srcdir/${pkgname%-git}/cmake/build"
  make install
}
