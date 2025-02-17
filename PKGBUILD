# Maintainer: Martin Reboredo <yakoyoku@gmail.com>

pkgname=mongosh
pkgver=2.2.10
pkgrel=1
pkgdesc='Rich Node.js REPL for interacting with MongoDB instances.'
arch=('x86_64')
url='https://github.com/mongodb-js/mongosh'
license=('Apache')
depends=(nodejs krb5)
makedepends=(git npm modclean libmongocrypt)
optdepends=('libmongocrypt: session encryption support')
source=(
  https://registry.npmjs.org/$pkgname/-/$pkgname-$pkgver.tgz
)
noextract=($pkgname-$pkgver.tgz)
sha256sums=('571cc0164d448bf84a722b389bad1fc5223cfe9375d4df512f6ee2454fa1e583')

package() {
  export PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=1
  npm install --omit=dev -g --prefix "$pkgdir"/usr "$srcdir"/$pkgname-$pkgver.tgz
  install -dm755 "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$pkgdir"/usr/lib/node_modules/$pkgname/LICENSE "$pkgdir"/usr/share/licenses/$pkgname

  cd "$pkgdir"/usr/lib/node_modules/$pkgname
  modclean --path . -r -a "*.ts,.bin,.deps,.github,.vscode,bin.js,makefile" -I "license,makefile*"

  # Non-deterministic race in npm gives 777 permissions to random directories.
  # See https://github.com/npm/npm/issues/9359 for details.
  chmod -R u=rwX,go=rX "$pkgdir"
  # npm installs package.json owned by build user
  # https://bugs.archlinux.org/task/63396
  chown -R root:root "$pkgdir"
}
