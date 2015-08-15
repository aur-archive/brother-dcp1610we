# Maintainer: Daniel Cisek <pl1230@gmail.com>

pkgname=brother-dcp1610we
pkgver=3.0.1
pkgrel=1
pkgdesc="Driver for the Brother DCP-1610we multifuncional printer"
arch=('i686' 'x86_64')
url="http://solutions.brother.com/linux/en_us/index.html"
license=('custom:brother')

if [ "$(uname -m)" = "x86_64" ]; then
 depends=('lib32-glibc' 'psutils')
else
	depends=('psutils')
fi

source=(
	http://download.brother.com/welcome/dlf101533/dcp1610wlpr-3.0.1-1.i386.deb
	http://download.brother.com/welcome/dlf101532/dcp1610wcupswrapper-3.0.1-1.i386.deb
)

md5sums=('f5c162bd48c79bacdce9e4f674903480'
         '783a9cbc258324d14b10bf91c718920e')

build() {
  srcdir="$startdir/src"
  mkdir -p "$srcdir" && cd "$srcdir"

  for i in $startdir/*.deb; do
    ar -x $i
    bsdtar xf data.tar.gz
  done
#  echo "Patching file for systemd compatibility"
#  patch $srcdir/opt/brother/Printers/DCP1610W/cupswrapper/cupswrapperdcpj132w < cupswrapper-systemd.patch
}

package() {
  srcdir="$startdir/src"
  cd $srcdir

  install -d -m755 "$pkgdir/usr/lib/cups/filter"
#  install -d -m755 "$pkgdir/usr/lib64/cups/filter"
  install -d -m755 "$pkgdir/usr/share/cups/model/Brother"
  install -d -m755 "$pkgdir/usr/share/ppd/Brother"
	
	
  cp -r "$srcdir/usr" "$pkgdir"
  cp -r "$srcdir/opt" "$pkgdir"
  cp "$srcdir/opt/brother/Printers/DCP1610W/cupswrapper/brother-DCP1610W-cups-en.ppd" "$pkgdir/usr/share/cups/model/Brother"
  cp "$srcdir/opt/brother/Printers/DCP1610W/cupswrapper/brother-DCP1610W-cups-en.ppd" "$pkgdir/usr/share/ppd/Brother"
  cp "$srcdir/opt/brother/Printers/DCP1610W/cupswrapper/brother_lpdwrapper_DCP1610W" "$pkgdir/usr/lib/cups/filter"
}
