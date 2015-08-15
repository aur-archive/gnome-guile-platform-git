# Contributor: Daniel Oliveira <psykond@gmail.com>
pkgname=gnome-guile-platform-git
pkgver=20101022
pkgrel=1
pkgdesc="Binding between Guile Scheme and the Gnome stack of libraries. (fe. Pango, GTK+, Cairo, GStreamer, Glade, GtkSourceView and else). To build wrappers for GTK+ and higher in the stack, you will first need Guile-Cairo."
arch=('i686', 'x86_64')
url="http://www.gnu.org/software/guile-gnome/"
license=('GPL2')
depends=('guile>=1.6.4' 'g-wrap>=1.9.13' libffi patch)
provides=('guile-gnome-platform')
makedepends=('git')

_gitroot="git://git.sv.gnu.org/guile-gnome.git"
_gitname="guile-gnome-platform"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  #
  # BUILD HERE
  #

  ./scripts/configure-packages guile-gnome-platform
  ./autogen.sh --prefix=/usr
  make || return 1
  make DESTDIR="$pkgdir/" install
}
