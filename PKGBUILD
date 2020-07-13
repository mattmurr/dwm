# $Id$
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	dwm-attachbottom-6.2.diff
	dwm-push_no_master-6.2.diff
	dwm-uselessgap-6.2.diff
  dwm-pertag-6.2.diff
  dwm-alwayscenter-20200625-f04cac6.diff
  enable-color-fonts.diff
	config.h
	dwm.desktop)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            '8a05d45f13a5852790f45a26a9c814b7ac28a917be8d3252b66970a39f68611e'
            '1398b82ebb891e5c47a91a023be66d08c92d1355fe5a6614bda570fea6b46e4f'
            '5667251372a5f3e8f297a2b458637ead9627f608b8e86e7a517baf791106a237'
            '055da0f12dbfde9e50df54e1f2d87966466404a36c056efb94bb21ab03b94b10'
            '5c91c14d598544533992a8bd6345c8fc39940678c276200ef17d8f20334bf8c3'
            '3bac812c74bfd71e7ee6536da5a369d31095d13de957a57a4702c3b3f2776744'
            'f66de3072601061a10883229a30f0f67fb57c8097760ffdd5f184866d3564e90'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  # Copy the config.h into the build directory
  cp "$srcdir/config.h" config.h

  # Apply the patches
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.diff ]] || continue
    echo "Applying patch $src..."
    patch -Np1 < "../$src"
  done
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
