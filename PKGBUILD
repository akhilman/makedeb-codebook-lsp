# Maintainer: Ildar Akhmetgaleev <akhilman@gmail.com>
# Original Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=codebook-lsp
pkgver=0.3.8
pkgrel=1
pkgdesc='Code-aware spell checker with language server implementation'
arch=(amd64)
url=https://github.com/blopker/codebook
license=(MIT)
depends=('libgcc-s1' 'libc6')
makedepends=('git' 'rustup' 'pkg-config' 'libssl-dev')
options=(!lto)
source=("codebook-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=('00198e830da8905af21c6504f6e123939e9d24bd671db9f8fcb093ec23bba86777092c251d17782bf48382b36c9b2d0e96a49013a7ec7d9c884207b603ed43ad')

prepare() {
  cd codebook-$pkgver
  rustup default stable
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd codebook-$pkgver
  cargo build --release --locked --offline
}

check() {
  cd codebook-$pkgver
  cargo test --locked --offline
}

package() {
  cd codebook-$pkgver
  install -Dt "$pkgdir"/usr/bin target/release/$pkgname
  install -Dt "$pkgdir"/usr/share/licenses/$pkgname LICENSE
}
