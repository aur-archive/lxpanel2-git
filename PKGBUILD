pkgname=lxpanel2-git
pkgver=20120508
pkgrel=1
pkgdesc="Lightweight X11 desktop panel (part of LXDE)."
arch=('i686' 'x86_64')
url="http://lxde.org/"
license=('GPL')
depends=('alsa-lib' 'gtk3' 'lxmenu-data' 'libwnck3' \
	 'menu-cache' 'startup-notification' 'libgtop')
makedepends=('vala' 'cmake' 'gcc' 'intltool' 'libtool' \
	     'make' 'pkgconfig' 'python' 'git')
options=('!libtool')
provides=('lxpanel2')
conflicts=('lxpanel2' 'lxpanel' 'lxpanel-git')
groups=('lxde-git')
source=()
md5sums=('')

_gitroot="git://lxde.git.sourceforge.net/gitroot/lxde/lxpanel2"
_gitname="lxpanel2"

build() {
  cd ${srcdir}

  msg "Connecting to GIT server...."

  if [ -d $startdir/src/$_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf $srcdir/$_gitname-build
  cp -r $srcdir/$_gitname $srcdir/$_gitname-build
  cd $srcdir/$_gitname-build

#  sed -i -e "s/pkg_check_modules(GTK REQUIRED gtk+-3.0)/pkg_check_modules(GTK REQUIRED gtk+-3.0 gio-unix-2.0) /" CMakeLists.txt
  cmake . -DCMAKE_INSTALL_PREFIX=/usr || return 1 
  make || return 1
  make DESTDIR=${pkgdir} install || return 1
}
