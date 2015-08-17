# $Id: PKGBUILD 17677 2010-05-24 20:39:22Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>

pkgname=ssh2
pkgver=2.0.13
pkgrel=6
pkgdesc="ssh implementation from ssh.com"
arch=(i686 x86_64)
url="http://www.ssh.com/"
license=('GPL')
depends=(zlib shadow libsm libx11)
makedepends=(xorg-xauth)
source=(http://archlinux-stuff.googlecode.com/files/ssh2_2.0.13.orig.tar.gz \
	http://archlinux-stuff.googlecode.com/files/ssh2_2.0.13-7.diff.gz)
md5sums=('1853aba4c7c9c501545c9e56a71fa9c3'
         '95579867c3a4f90d839ebd4f18ca2cee')

build() {
  cd $srcdir/ssh-${pkgver}
  patch -Np1 <../ssh2_$pkgver-7.diff
  sed -i 's#i\[3456\]86-\*#x86_64-\* | i\[3456\]86-\*#' config.sub
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --includedir=/usr/include/ssh2 \
	--enable-tcp-port-forwarding \
	--enable-X11-forwarding \
	--without-pgp \
	--with-x
  make || return 1
  make DESTDIR=$pkgdir install || return 1

  mkdir -p $pkgdir/usr/share && \
  mv $pkgdir/usr/man $startdir/pkg/usr/share/ || return 1

  rm -f $pkgdir/usr/bin/scp \
	$pkgdir/usr/bin/sftp \
	$pkgdir/usr/bin/sftp-server \
	$pkgdir/usr/bin/ssh-askpass \
	$pkgdir/usr/bin/ssh-signer \
	$pkgdir/usr/bin/ssh \
	$pkgdir/usr/bin/ssh-add \
	$pkgdir/usr/bin/ssh-agent \
	$pkgdir/usr/bin/ssh-keygen \
	$pkgdir/usr/share/man/man1/scp.1 \
	$pkgdir/usr/share/man/man1/sftp.1 \
	$pkgdir/usr/share/man/man1/ssh-add.1 \
	$pkgdir/usr/share/man/man1/ssh-agent.1 \
	$pkgdir/usr/share/man/man1/ssh-keygen.1 \
	$pkgdir/usr/share/man/man1/ssh.1 \
	$pkgdir/usr/share/man/man8/sshd.8 \
	$pkgdir/usr/sbin/sshd
}
