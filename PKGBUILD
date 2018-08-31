# Maintainer: Jan Boelsche <jan@lagomorph.de>

pkgname=ssb-pacman-git
pkgver=1.0.0.r56.2b1b67a
pkgrel=2
pkgdesc="Secure-Scuttlebutt-based pacman back-end for reproducable installs"
arch=('x86_64')
url=""
license=('GPL')
groups=()
depends=(
  'scuttlebot'
  'ssb-autofollow-git'
  'ssb-autoname'
)
makedepends=('git' 'npm')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=()
install=${pkgname}.install
source=('ssb-pacman.service' 'git+ssh://git@github.com/regular/ssb-pacman.git')
noextract=()

sha256sums=('96144304d74c806992abcc54a8c2cda249aa49d68b5288a7b737cfc40190b264'
            'SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
  printf "%s.r%s.%s" "$(node -e 'console.log(require("./package.json").version)')" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package () {
  install -Dm 644 -t "${pkgdir}/usr/lib/systemd/system" "ssb-pacman.service"
  install -Dm 775 -d "${pkgdir}/var/ssb-pacman/node_modules"

	cd "$srcdir/${pkgname%-git}"
  install -Dm 644 -T "sbot.config" "${pkgdir}/etc/ssb-pacman/config"

  source "$HOME/.nvm/nvm.sh"
  nvm use 10.8.0
  local _npmdir="${pkgdir}/usr/lib/node_modules/"
  mkdir -p $_npmdir
  npm install -g --prefix "${pkgdir}/usr" regular/ssb-pacman
  for plugin in ssb-pacman ssb-autofollow ssb-autoname; do
    ln -s "/usr/lib/node_modules/${plugin}" "${pkgdir}/var/ssb-pacman/node_modules/"
  done
}
