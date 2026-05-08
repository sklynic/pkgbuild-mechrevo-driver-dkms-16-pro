# Maintainer: Shiina Rikka <rikka@rikka.im>
# Contributor: sklynic
_pkgname=mechrevo-drivers
pkgname=mechrevo-drivers-dkms
pkgver=4.22.2
pkgrel=1
pkgdesc='Kernel modules for MECHREVO devices. Drivers for several platform devices for MECHREVO notebooks meant for DKMS. Modified from TUXEDO drivers.'
arch=('x86_64')
url='https://gitlab.com/tuxedocomputers/development/packages/tuxedo-drivers'
license=('GPL-2.0+')
depends=('dkms')
provides=('tuxedo-drivers-dkms'
	          'tuxedo-keyboard'
            'tuxedo-keyboard-ite'
            'tuxedo-io'
            'clevo-wmi'
            'clevo-acpi'
            'uniwill-wmi'
            'ite_8291'
            'ite_8291_lb'
            'ite_8297'
            'ite_829x')
conflicts=('tuxedo-drivers-dkms' 'tuxedo-keyboard-dkms' 'tuxedo-keyboard-ite-dkms')
source=($pkgname-$pkgver.tar.gz::https://gitlab.com/tuxedocomputers/development/packages/tuxedo-drivers/-/archive/v$pkgver/tuxedo-drivers-v$pkgver.tar.gz dkms.conf patch.diff )
sha256sums=('4068ae8fc01c960f18b79d6b47cfc515e21be4abecbeda17746b59c1f9ae96aa'
            'd955ba6609666364eb63b073fd7bd9f5397de523e39226eb1b1fe866b4567a4e'
            '62912e681158257f7309fb234376e59ecf6620869e58f76d85d854a5f13b50c5')

prepare(){
  cd "${srcdir}/tuxedo-drivers-v$pkgver"
	patch -Np1 -i ../patch.diff
}

package() {
  install -Dm644 "$srcdir"/dkms.conf "$pkgdir/usr/src/${pkgname%-dkms}-$pkgver/dkms.conf"
  sed -i "s/#MODULE_VERSION#/$pkgver/g" "$pkgdir/usr/src/${pkgname%-dkms}-$pkgver/dkms.conf"

  install -Dm644 "tuxedo-drivers-v$pkgver"/files/usr/lib/modprobe.d/*.conf -t "$pkgdir/usr/lib/modprobe.d/"
  install -Dm644 "tuxedo-drivers-v$pkgver"/files/usr/lib/udev/rules.d/*.rules -t "$pkgdir/usr/lib/udev/rules.d/"
  install -Dm644 "tuxedo-drivers-v$pkgver"/files/usr/lib/udev/hwdb.d/*.hwdb -t "$pkgdir/usr/lib/udev/hwdb.d/"

  mkdir -p "${pkgdir}/usr/src/${_pkgname}-${pkgver}"
  cp -ar "tuxedo-drivers-v$pkgver"/src/* "$pkgdir/usr/src/${_pkgname%}-$pkgver/"
}
