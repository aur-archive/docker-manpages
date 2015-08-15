# Maintainer: xduugu
pkgname=docker-manpages
pkgver=1.6.2
pkgrel=1
pkgdesc='Man pages for docker'
arch=('any')
url='http://www.docker.io/'
license=('Apache')
depends=('docker')
makedepends=('git' 'go')
source=("git+https://github.com/docker/docker.git#tag=v$pkgver"
        # for man pages
        "git+https://github.com/cpuguy83/go-md2man.git"
        "git+https://github.com/russross/blackfriday.git"
        "git+https://github.com/shurcooL/sanitized_anchor_name.git")
md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

prepare() {
  # for man page generation
  for d in cpuguy83/go-md2man russross/blackfriday shurcooL/sanitized_anchor_name; do
    mkdir -p "go/src/github.com/${d%%/*}"
    ln -s "$srcdir/${d##*/}" "go/src/github.com/$d"
  done
}

build() {
  cd docker

  # build helper for man page generation
  GOPATH="$srcdir/go" go install github.com/cpuguy83/go-md2man

  # generate man pages
  PATH="$srcdir/go/bin:$PATH" docs/man/md2man-all.sh -q
}

package() {
  cd docker
  install -dm755 "$pkgdir/usr/share/man"
  mv docs/man/man{1,5} "$pkgdir/usr/share/man"
}

# vim:set ts=2 sw=2 et:
