# Mantainer: None. PKGBUILD adapated from https://aur.archlinux.org/packages/brother-hll2370dn
_model=HLL2400DW
pkgname=brother-${_model,,}
pkgver=4.1.0
pkgrel=1
pkgdesc="Brother ${_model} CUPS driver"
arch=('i686' 'x86_64')
url='http://welcome.solutions.brother.com/bsc/public_s/id/linux/en/index.html'
license=('GPL')
depends=('cups' 'perl')
source=(http://download.brother.com/welcome/dlf105948/${_model,,}pdrv-$pkgver-1.i386.rpm)
sha256sums=('e08a1756abc1aaa4959b6f5259108e2053753322b7710944db34f153e585bf5a')

package() {
  # using /usr/share instead of /opt
  echo "$pkgdir"
  mkdir -p "$pkgdir/usr/share"
  cp -R "$srcdir/opt/brother" "$pkgdir/usr/share"
  sed -i 's|\\\/opt\\\/|\\\/usr\\\/|' "$pkgdir/usr/share/brother/Printers/${_model}/cupswrapper/lpdwrapper"
  sed -i 's|\\\/opt\\\/|\\\/usr\\\/|' "$pkgdir/usr/share/brother/Printers/${_model}/lpd/lpdfilter"

  # symlink for lpdwrapper so it correctly figures out the printer model from the path
  install -d "$pkgdir/usr/lib/cups/filter/"
  ln -s "/usr/share/brother/Printers/${_model}/cupswrapper/lpdwrapper" "$pkgdir/usr/lib/cups/filter/brother_lpdwrapper_${_model}"

  # symlink for the PPD
  install -d "$pkgdir/usr/share/cups/model/"
  ln -s "/usr/share/brother/Printers/${_model}/cupswrapper/brother-${_model}-cups-en.ppd" "$pkgdir/usr/share/cups/model/"

  # a couple architecture-specific symlinks
  ln -s "/usr/share/brother/Printers/${_model}/lpd/$CARCH/brprintconflsr3" "$pkgdir/usr/share/brother/Printers/${_model}/lpd/"
  ln -s "/usr/share/brother/Printers/${_model}/lpd/$CARCH/rawtobr3" "$pkgdir/usr/share/brother/Printers/${_model}/lpd/"

  # # symlink for inf because it tries to execute it there
  # ln -s "/usr/share/brother/Printers/${_model}/inf" "$pkgdir/usr/share/brother/Printers/${_model}/lpd/"
}

