# Contributor: Abdallah Aly < l3thal8 @gmail.com>
pkgname=falcon-sdl-svn
pkgver=113
pkgrel=1
pkgdesc="the SDL module for Falcon proramming language"
license=('custom:"GPLv2 or Falcon Programming Language License"')
url="http://www.falconpl.org"
arch=(i686 x86_64)
makedepends=('cmake' 'subversion')
depends=('falcon' 'sdl' 'sdl_gfx' 'sdl_sound' 'sdl_mixer' 'sdl_image' 'sdl_ttf' )
provides=('falcon-sdl')

_svntrunk=svn://falconpl.org/falcon/modules/sdl/trunk/
_svnmod=sdl

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  cmake . || return 1
  make || return 1
  mkdir -p $startdir/pkg/usr/lib/falcon || return 1
  make DESTDIR="$startdir/pkg/" install || return 1
  mkdir -p $startdir/pkg/usr/share/licenses/falcon || return 1
  cp LICENSE $startdir/pkg/usr/share/licenses/falcon/falcon-sdl || return 1

}
