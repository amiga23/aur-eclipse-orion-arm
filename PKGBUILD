# Maintainer: Thomas Scheller <t.scheller@email.de>
#
# Repository: https://github.com/amiga23/aur-eclipse-orion-arm

pkgname=eclipse-orion-arm
pkgver=12
pkgrel=0
epoch=
pkgdesc="Open Source Platform for Cloud Based Development"
arch=('armv7h' 'aarch64')
url="http://www.eclipse.org/orion"
license=('EPL')
groups=()
depends=(java-runtime)
makedepends=()
checkdepends=()
optdepends=()
provides=(eclipse-orion)
conflicts=()
replaces=()
backup=('etc/conf.d/eclipse-orion')
options=()
install=install
changelog=changelog
source=('http://ftp-stud.fht-esslingen.de/pub/Mirrors/eclipse/orion/drops/R-12.0-201606220105/eclipse-orion-12.0-linux.gtk.x86_64.zip'
        'sysuser.conf'
	'eclipse-orion.conf'
	'eclipse-orion.service'
	'orion.sh')
noextract=()
sha256sums=('42ccb836caa59211e6b2929ba6a146fbd58be50f637c2c74041991864fac2d22'
            '415cb479c52ebbbe955ee577881133be77db46d728e408454ac605fa01fa618f'
	    '41239374b71c78944a62d734cd14ddd010aac7bb5f3f1ce66740ab5472ca51a2'
	    'f2fbf4d8fb9d8626ec0b9a8818c888284a8e420915f1fe5981be30be6f1ee455'
	    'ca28188c4daa89477c1928d0792a567fd8d2e9eebdb06a3e30f3a8bf0e9dc441')
package() {
  # Remove non ARM binaries
  rm $srcdir/eclipse/orion
  rm -R $srcdir/eclipse/plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64*
  
  # install
  mkdir -p $pkgdir/usr/share
  mv $srcdir/eclipse $pkgdir/usr/share/eclipse-orion
  cp -L $srcdir/orion.sh $pkgdir/usr/share/eclipse-orion/orion.sh
  
  # setup eclipse-orion home
  install -m 755 -d $pkgdir/var/lib/eclipse-orion
  install -m 755 -d $pkgdir/var/lib/eclipse-orion/workspace
  ln -s /var/lib/eclipse-orion/workspace $pkgdir/usr/share/eclipse-orion/workspace
  
  # create user (creation itself is done with install script)
  install -D -m 644 $srcdir/sysuser.conf "$pkgdir"/usr/lib/sysusers.d/eclipse-orion.conf

  # install service
  install -Dm0644 $srcdir/eclipse-orion.service $pkgdir/usr/lib/systemd/system/eclipse-orion.service
  install -Dm0644 $srcdir/eclipse-orion.conf $pkgdir/etc/conf.d/eclipse-orion
}
