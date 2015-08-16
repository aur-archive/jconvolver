# Contributor: Stefan Husmann <stefan-husmann@t-online.de>
# Maintainer: Philipp Überbacher <hollunder at gmx dot at>
pkgname=jconvolver
pkgver=0.9.2
pkgrel=2
pkgdesc="Convolution Engine for JACK, including example config and reverbs files"
url="http://kokkinizita.linuxaudio.org/linuxaudio/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('zita-convolver>=3.0.2' 'clthreads>=2.4.0' 'jack')
install=${pkgname}.install
source=(http://kokkinizita.linuxaudio.org/linuxaudio/downloads/${pkgname}-${pkgver}.tar.bz2 \
http://kokkinizita.linuxaudio.org/linuxaudio/downloads/${pkgname}-reverbs.tar.bz2)
md5sums=('f1a33f0f455961a7b21b56bdb0f725b1'
         'a33ec6a97fac039400f7674f3bde4ca9')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}/source"

  sed -i 's/usr\/local/usr/' Makefile

  make SUFFIX=""
}

package(){
  cd "${srcdir}/${pkgname}-${pkgver}/source"

  make SUFFIX="" PREFIX="/usr" DESTDIR=${pkgdir} install

  #this installs the configuration readme
  install -Dm 644 ../README.CONFIG "${pkgdir}/usr/share/jconvolver/README.CONFIG"

  #this installs the example config files and reverbs that come with jconv
  cp -r ../config-files/ "${pkgdir}/usr/share/jconvolver/"

  #this installs additional reverbs
  cp -r ${srcdir}/reverbs/* "${pkgdir}/usr/share/jconvolver/config-files/"

  #fix permissions for super-stereo.conf
  chmod 644 "${pkgdir}/usr/share/jconvolver/config-files/ambisonic/super-stereo.conf"
}
