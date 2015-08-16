#Maintainer:	Jesse	Jaara		<gmail.com: jesse.jaara>
#Contributor:	Aaron	Griffin		<archlinux.org: aaron>
#Contributor:	Tobias	Powalowski	<archlinux.org: tpowa>
#Contributor:	Thomas	Bächler		<archlinux.org: thomas>

pkgname=lib32-udev
pkgver=182
pkgrel=2
arch=('x86_64')
pkgdesc="The userspace dev tools (udev) (32-bit)"
url="http://www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html"
license=('GPL')
options=(!makeflags !libtool)
depends=('lib32-glib2')
makedepends=('gcc-multilib' 'gperf' 'lib32-acl' 'lib32-kmod' 'lib32-util-linux')
source=(ftp://ftp.kernel.org/pub/linux/utils/kernel/hotplug/udev-${pkgver}.tar.xz
	0001-split-usr-always-read-config-files-from-lib-udev.patch
	0002-reinstate-TIMEOUT-handling.patch)

build() {
  export CC="gcc -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd "${srcdir}/udev-${pkgver}"

  patch -p1 -i ../0001-split-usr-always-read-config-files-from-lib-udev.patch
  patch -p1 -i ../0002-reinstate-TIMEOUT-handling.patch

  ./configure --prefix=/usr \
              --with-rootprefix= \
              --sysconfdir=/etc \
              --libdir=/usr/lib32 \
              --libexecdir=/lib32 \
	      --disable-introspection \
              --with-systemdsystemunitdir=/usr/lib/systemd/system \
              --with-firmware-path=/usr/lib/firmware/updates:/lib/firmware/updates:/usr/lib/firmware:/lib/firmware
  make
}

package() {
    cd "${srcdir}/udev-${pkgver}"

  make DESTDIR="${pkgdir}" install
  rm -rf "${pkgdir}"/{etc,lib32,lib,usr/{include,lib,bin,share}}
}

md5sums=('023877e6cc0d907994b8c648beab542b'
         '7c08a9f642d04705c6d8545c50a14b50'
         '61d784555b0cca1b6321270ba0a09938')
