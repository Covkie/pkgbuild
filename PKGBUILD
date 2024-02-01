# Maintainer: edu4rdshl <edu4rdshl[dot]protonmail.com>
# Submitter: picokan <todaysoracle@protonmail.com>
pkgname=vesktop
_pkgname=Vesktop
pkgdesc="A standalone Electron app that loads Discord & Vencord"
pkgver=1.5.0
pkgrel=15
arch=('x86_64' 'aarch64')
url="https://github.com/Vencord/Vesktop"
license=('GPL3')
depends=('electron')
makedepends=('pnpm' 'git')
optdepends=(
  'libnotify: Notifications'
  'xdg-utils: Open links, files, etc'
  'xdg-desktop-portal: Screensharing with Wayland'
)
provides=('vencord')
conflicts=('vencord')
source=("${url}/archive/refs/tags/v${pkgver}.tar.gz"
        'vesktop.desktop'
        'vesktop.sh')
sha256sums=('7f20edeb4612386ae98d5dccfa4b37ad1f5336d4551de3375c3b16e81925b10a'
            'f279b1e469fb965cdf6dba9b4f428b0a7f28f414d84a47c6481b726adeb99c2b'
            '58c61ef14e5eaefe7207a6b66b065973a6002a2ae1d0fb9fd8ec2d2c2b198607')
prepare() {
  # Use system's electron
  sed -i '/linux/s/^/        "electronDist": "\/usr\/lib\/electron",\n/' "$srcdir/$_pkgname-$pkgver/package.json"
}

build() {
  cd "$_pkgname-$pkgver"

  pnpm i
  pnpm package:dir
}

package() {
  cd "$srcdir"

  install -d "${pkgdir}/usr/lib/${pkgname}"
  install -d "${pkgdir}/usr/bin"

  cp "$_pkgname-$pkgver/dist/linux-unpacked/resources/app.asar" "${pkgdir}/usr/lib/${pkgname}/"
  install -Dm755 "./vesktop.sh" "$pkgdir/usr/bin/vesktop"

  install -Dm 644 "vesktop.desktop" "$pkgdir/usr/share/applications/vesktop.desktop"
  install -Dm 644 "$_pkgname-$pkgver/static/icon.png" "$pkgdir/usr/share/pixmaps/${pkgname}.png"
  install -Dm 644 "$_pkgname-$pkgver/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

