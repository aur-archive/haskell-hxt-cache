# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=hxt-cache
pkgname=haskell-hxt-cache
pkgver=9.0.0
pkgrel=3
pkgdesc="Cache for HXT XML Documents and other binary data"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:OtherLicense')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-sha<2' 'haskell-binary<1' 'haskell-bytestring=0.9.1.7' 'haskell-containers=0.3.0.0' 'haskell-deepseq=1.1.0.0' 'haskell-directory=1.0.1.1' 'haskell-filepath=1.1.0.4' 'haskell-haskell98=1.0.1.1' 'haskell-hxt<10' 'haskell-old-locale=1.0.0.2' 'haskell-old-time=1.0.0.5' 'haskell-unix=2.4.0.2')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
md5sums=('b9cb880a40d7d480f0703ba2422ef289')
