# Maintainer: Ildar Akhmetgaleev <akhilman@gmail.com>
# Original Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=codebook-lsp
pkgver=0.3.30
pkgrel=1
pkgdesc='Code-aware spell checker with language server implementation'
arch=(amd64)
url=https://github.com/blopker/codebook
license=(MIT)
depends=('libgcc-s1' 'libc6')
makedepends=('git' 'rustup' 'pkg-config' 'libssl-dev')
options=(!lto)
source=("codebook-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=('2ea835f6d94f38df9227f098ec0193b448e6649b81d49fc3fbe839cdfd268e81ba702980c9900348d84b67f77c5b84105f04f0e23a918ebe53d1fc5790b07d88')

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
