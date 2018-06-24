# Maintainer: BlackIkeEagle <ike DOT devolder AT gmail DOT com>
# Contributor: (sirocco AT ngs.ru)

pkgbase=doublecmd-svn
_svnmod=doublecmd
pkgname=('doublecmd-svn-gtk2' 'doublecmd-svn-qt5')
pkgver=8184
pkgrel=1
url="http://doublecmd.sourceforge.net/"
arch=('x86_64')
license=('GPL')
provides=('doublecmd')
conflicts=('doublecmd')
makedepends=('lazarus' 'qt5pas' 'gtk2' 'subversion')
optdepends=(
	'lua51: scripting'
    'unzip: support extracting zip archives'
    'zip: suport packing zip archives'
	'p7zip: support for 7zip archives'
	'libunrar: support for rar archives'
)
source=(
	"$_svnmod::svn://svn.code.sf.net/p/doublecmd/code/trunk"
)
sha512sums=(
	'SKIP'
)

pkgver() {
	cd "$srcdir/$_svnmod"
	svnversion | tr -d [A-z]
}

prepare() {
    cp -a /usr/lib/lazarus ./

	cd "$_svnmod"
    sed -e 's/LIB_SUFFIX=.*/LIB_SUFFIX=/g' -i install/linux/install.sh
    sed -e "s@=\$(which lazbuild)@=\"\$(which lazbuild) --lazarusdir=$srcdir/lazarus\"@" -i build.sh

	cd "$srcdir"

    cp -a "$_svnmod" "$pkgbase-gtk"
    cp -a "$_svnmod" "$pkgbase-qt5"
}

build() {
    msg2 'build gtk'
    cd "$srcdir/$pkgbase-gtk"
    ./build.sh beta gtk2

    msg2 'build qt5'
    cd "$srcdir/$pkgbase-qt5"
    ./build.sh beta qt5
}

package_doublecmd-svn-gtk2() {
	pkgdesc="twin-panel (commander-style) file manager (GTK)"
    depends=('gtk2' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-qt5')
    provides+=('doublecmd-gtk2')
	cd "$srcdir/$pkgbase-gtk"
	./install/linux/install.sh --install-prefix="$pkgdir"
}

package_doublecmd-svn-qt5() {
	pkgdesc="twin-panel (commander-style) file manager (Qt5)"
    depends=('qt4pas' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-gtk2')
    provides+=('doublecmd-qt5')
    replaces=('doublecmd-svn-qt4' 'doublecmd-svn-qt')
	cd "$srcdir/$pkgbase-qt5"
	./install/linux/install.sh --install-prefix="$pkgdir"
}
