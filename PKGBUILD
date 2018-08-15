# Maintainer: Jan Boelsche <jan@lagomorph.de>

pkgname=ssb-pacman-git
pkgver=1.0.0.r53.20c743f
pkgrel=1
pkgdesc="Secure-Scuttlebutt-based pacman backend for reproducable installs"
arch=('x86_64')
url=""
license=('GPL')
groups=()
depends=('scuttlebot')
makedepends=('git' 'npm')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=()
install=${pkgname}.install
source=('ssb-pacman.service' 'config' 'git+ssh://git@github.com/regular/ssb-pacman.git')
noextract=()

sha256sums=('462f043028a87c444bdc26880d0a7cdc6a3061640a8337616d7a36d643412248'
            '2d198038f419c5bda2a30addb06c7337cebe05ec529afe18413a34ba43d14cbf'
            'SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
  printf "%s.r%s.%s" "$(node -e 'console.log(require("./package.json").version)')" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package () {
  install -Dm 644 -t "${pkgdir}/usr/lib/systemd/system" "ssb-pacman.service"
  install -Dm 644 -t "${pkgdir}/etc/ssb-pacman" "config"
  install -Dm 775 -d "${pkgdir}/var/ssb-pacman/node_modules"

  source "$HOME/.nvm/nvm.sh"
  nvm use 10.8.0
	cd "$srcdir/${pkgname%-git}"
  local _npmdir="${pkgdir}/usr/lib/node_modules/"
  mkdir -p $_npmdir
  npm install -g --prefix "${pkgdir}/usr" regular/ssb-pacman
  ln -s /usr/lib/node_modules/ssb-pacman "${pkgdir}/var/ssb-pacman/node_modules/"
}
