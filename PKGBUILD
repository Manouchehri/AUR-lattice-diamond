# Maintainer: doragasu <doragasu (yawn) hotmail (roll) com>
# Contributor: David Manouchehri

pkgname="lattice-diamond"
pkgdesc="Lattice Diamond design software"
url="http://www.latticesemi.com/"
license=('custom')
pkgver=3.9
arch=('x86_64')
source=("http://files.latticesemi.com/Diamond/${pkgver}/diamond_${pkgver/"."/"_"}-base_x64-99-2-${arch}-linux.rpm"
		"synp-plat-check.patch"
		"lattice-diamond.png"
		"lattice-diamond.desktop")
makedepends=('rpmextract')
sha512sums=('SKIP')
# depends=('')
pkgrel=1
options=('!strip' '!upx')
PKGEXT=".pkg.tar"

pkgver() {
	cd "${srcdir}/${_gitname}"
	(
		set -o pipefail
		git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
		printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
	)
}

prepare() {
	# Extract all the packages
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/bin
	tar -xzf bin.tar.gz
	rm bin.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/cae_library
	tar -xzf cae_library.tar.gz
	rm cae_library.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/data
	tar -xzf data.tar.gz
	rm data.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/embedded_source
	tar -xzf embedded_source.tar.gz
	rm embedded_source.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/examples
	tar -xzf examples.tar.gz
	rm examples.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/ispfpga
	tar -xzf ispfpga.tar.gz
	rm ispfpga.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/synpbase
	tar -xzf synpbase.tar.gz
	rm synpbase.tar.gz
	cd ${srcdir}/usr/local/diamond/${pkgver}_x64/tcltk
	tar -xzf tcltk.tar.gz
	rm tcltk.tar.gz
}

build() {
	# Patch to skip platform check, allowing Synplify Pro to run on non
	# officially supported platforms
	# patch -p1 < synp-plat-check.patch
	echo
}

package() {
	# Move everything to pkgdir
	mv ${srcdir}/usr ${pkgdir}/
	# Copy .desktop and icon files
	mkdir -p "${pkgdir}/usr/share/pixmaps"
	cp "${srcdir}/lattice-diamond.png" "${pkgdir}/usr/share/pixmaps"
	mkdir -p "${pkgdir}/usr/share/applications"
	cp "$srcdir/lattice-diamond.desktop" "$pkgdir/usr/share/applications/"
} 

