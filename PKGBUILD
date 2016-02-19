# Maintainer: Vanush Misha Paturyan <ektich+cfengine-aur@gmail.com>
# https://github.com/zizzfizzix/pkgbuilds
#
# Contributor: Kuba Serafinowski <zizzfizzix AT gmail DOT com>
# Contributor: Phillip Smith <fukawi2@NO-SPAM.gmail.com>
# Contributor: Christian Berendt <christian@thorlin.de>

pkgname=cfengine
pkgver=3.7.2
pkgrel=1
pkgdesc='Automated suite of programs for configuring and maintaining Unix-like computers.'
url='http://www.cfengine.org'
license=('GPL3')
arch=('i686' 'x86_64')
depends=('lmdb' 'openssl' 'pcre' 'libxml2')
makedepends=('which')
optdepends=('libvirt' 'postgresql-libs' 'libmariadbclient' 'acl')
install=${pkgname}.install
source=("${pkgname}-${pkgver}.tar.gz::https://cfengine-package-repos.s3.amazonaws.com/tarballs/${pkgname}-${pkgver}.tar.gz"
        "https://cfengine-package-repos.s3.amazonaws.com/tarballs/cfengine-masterfiles-${pkgver}.tar.gz"
        'cf-execd.service'
        'cf-monitord.service'
        'cf-serverd.service')
md5sums=('aff92abe87a5424680afd285d0384bef'
         'dba17dc5133b8fa86de11577120d46c5'
         'dba17dc5133b8fa86de11577120d46c5'
         'a2f9db31408f288cb934397ffb474db3'
         'ff28f7de9b81b4673082a2640a318896')

build() {
	cd ${srcdir}/${pkgname}-${pkgver}

  ./configure \
    --prefix=/usr \
    --with-workdir=/var/${pkgname} \
    --with-openssl \
    --with-pcre \
    --with-libacl=check \
    --with-libxml2 \
    --with-libvirt=check \
    --with-lmdb \
    --with-mysql=check \
    --with-postgresql=check

  make
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver}

	make DESTDIR=$pkgdir install

	install -D -m644 ${srcdir}/cf-execd.service \
		${pkgdir}/usr/lib/systemd/system/cf-execd.service
	install -D -m644 ${srcdir}/cf-serverd.service \
		${pkgdir}/usr/lib/systemd/system/cf-serverd.service
	install -D -m644 ${srcdir}/cf-monitord.service \
		${pkgdir}/usr/lib/systemd/system/cf-monitord.service
}

# vim:set ts=2 sw=2 et:
