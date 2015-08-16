# $Id:$
# Adapted from standard gdb package 
# Maintainer: Alexander 'hatred' Drozdov <adrozdoff@gmail.com>

pkgname=mingw32-gdb
_pkgname=gdb
pkgver=7.5.1
pkgrel=1
pkgdesc="The GNU Debugger for mingw32 targets"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/gdb/"
license=('GPL3')
depends=('ncurses' 'expat' 'python2' "gdb=$pkgver")
makedepends=('texinfo')
backup=('usr/i486-mingw32/etc/gdb/gdbinit')
options=('!libtool')
#install=gdb.install
source=(http://ftp.gnu.org/gnu/gdb/${_pkgname}-${pkgver}.tar.bz2{,.sig})

build() {
  cd ${srcdir}/${_pkgname}-${pkgver}

  unset LDFLAGS

  ./configure --prefix=/usr \
    --target=i486-mingw32 \
    --host=$CHOST \
    --build=$CHOST \
    --disable-nls \
    --with-system-readline \
    --enable-shared \
    --with-system-gdbinit=/usr/i486-mingw32/etc/gdb/gdbinit
  
  make
}

package() {
  cd ${srcdir}/${_pkgname}-${pkgver}
  make DESTDIR=${pkgdir} install

  # install "custom" system gdbinit
  install -dm755 $pkgdir/usr/i486-mingw32/etc/gdb
  touch $pkgdir/usr/i486-mingw32/etc/gdb/gdbinit

  # resolve conflicts with binutils
  rm ${pkgdir}/usr/x86_64-unknown-linux-gnu/i486-mingw32/include/{ansidecl,bfd,bfdlink,dis-asm,symcat}.h
  rm ${pkgdir}/usr/x86_64-unknown-linux-gnu/i486-mingw32/lib/{libbfd,libopcodes}.a
  rm ${pkgdir}/usr/x86_64-unknown-linux-gnu/i486-mingw32/lib/{libbfd,libopcodes}.so
  rm ${pkgdir}/usr/lib/libiberty.a
  rm ${pkgdir}/usr/share/info/{bfd,configure,standards}.info
  rm -r ${pkgdir}/usr/share/gdb/{python,syscalls}
  rm    ${pkgdir}/usr/share/info/*
  rm -r ${pkgdir}/usr/include/gdb/jit-reader.h
}

md5sums=('3f48f468b24447cf24820054ff6e85b1'
         '31ab569c78a01d3f946c6fe0336175fe')
