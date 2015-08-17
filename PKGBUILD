# Maintainer: Liganic <liganic-aur@gmx.net>
pkgname=tmx2lua-git
_pkgname=tmx2lua
pkgver=20121209
pkgrel=1
pkgdesc="Convert TMX files into Lua scripts"
arch=('i386' 'x86_64')
url="https://github.com/kyleconroy/tmx2lua"
license=('unknown')
groups=()
depends=()
makedepends=('git' 'go')
provides=($_pkgname)

_gitroot=git://github.com/hawkthorne/$_pkgname.git
_gitname=$_pkgname

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone --depth=1 "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  cp -r "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  export GOPATH="$srcdir/$_gitname-build/build/"
  go get
  go build -o $_pkgname
}

package() {
  mkdir -p "$pkgdir/usr/bin/"
  install -Dm755 "$srcdir/$_gitname-build/$_pkgname" "$pkgdir/usr/bin/"
}

# vim:set ts=2 sw=2 et:
