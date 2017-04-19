# Maintainer: doragasu <doragasu (yawn) hotmail (roll) com>
# Contributor: David Manouchehri

pkgname="lattice-diamond"
pkgdesc="Lattice Diamond design software"
url="http://www.latticesemi.com/"
license=('custom')
pkgver=3.9
_revision="99-2"
pkgrel=1
arch=('x86_64')
source=("http://files.latticesemi.com/Diamond/${pkgver}/diamond_${pkgver/"."/"_"}-base_x64-${_revision}-${arch}-linux.rpm"
		"synp-plat-check.patch"
		"lattice-diamond.png"
		"lattice-diamond.desktop")
makedepends=('rpmextract')
sha512sums=('ee4ef401f7e6db6b54061e612224666ee0f3218499653f82b66a2865a0fdf3e6c8986c7a70d6c92da7d1276b6e21081866603d544d6fdc0c60fcccbcfa7b683a'
			'85ca821cd2c090f3d953dd383b0059c9834786686e34094faa4bc875f1d31c7703c922edad37f1e0a4500699d1c0066e17b242e1ea5901783f8b313ceb4010d5'
			'772fa260bb1a4ed7c4e328a99b3cd16b625e8880d7731abbe0cd59dbe4d743265e169a26ceba7b619a87c1cb9638a268a5501d3358863171ee808e59b2d3b0ac'
			'1ead272db9c7a80bfd8b934424345da232909e196d8699266e7c1f0b994906fb32eca011d2257e76cc2d805609f0bba81f896a677bdfa35f4d9340f3163cdf66')
# depends=('')
options=('!strip' '!upx')
PKGEXT=".pkg.tar" # The package is over 3 GB, don't compress it.

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
	echo "Skipping Synplify patch.."
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

