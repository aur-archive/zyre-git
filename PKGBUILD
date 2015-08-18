# Contributor: Patrick Hanckmann <hanckmann at gmail.com>
# Maintainer: Patrick Hanckmann <hanckmann at gmail.com>
pkgname=zyre-git
pkgver=1.0.0
pkgrel=2
pkgdesc="Zyre - an open-source framework for proximity-based peer-to-peer applications (ZeroMQ)"
arch=(i686 x86_64)
url="https://github.com/zeromq/zyre"
license=('LGPL')
depends=('czmq-git')
makedepends=('git')
provides=(zyre)
conflicts=(zyre)
options=(!libtool)

_gitroot="git://github.com/zeromq/zyre.git"
_gitname="zyre"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."
  rm -rf "$srcdir/$_gitname"

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  # switch to tag v1.0.0
  cd "$srcdir/$_gitname"
  git checkout v1.0.0

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  #
  # BUILD HERE
  #

  ./autogen.sh
  ./configure --prefix=/usr
  make
} 

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
} 
