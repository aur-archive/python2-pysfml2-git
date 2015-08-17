# Maintainer: Thomas Glamsch <thomas.glamsch@gmail.com>
# Contributer: Philippe Huerlimann <phihue@gmail.com>
pkgname=python2-pysfml2-git
pkgver=20130304
pkgrel=2
pkgdesc="A Python 2 binding for SFML 2, written with Cython."
arch=('i686' 'x86_64')
url="http://pysfml2-cython.readthedocs.org/"
license=('BSD')
depends=('sfml-git' 'python2')
makedepends=('cython2' 'git')
source=()
md5sums=() 
_gitroot='git://github.com/bastienleonard/pysfml-cython.git'
_gitname='pysfml2-cython'

build() {
	cd "$srcdir"
	msg "Connecting to GIT server...."

	if [ -d $_gitname ] ; then
		cd $_gitname && git pull origin
		msg "The local files are updated."
	else
		git clone $_gitroot $_gitname
	fi

	msg "GIT checkout done or server timeout"
	msg "Starting make..."

	rm -rf "$srcdir/$_gitname-build"
	git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
	cd "$srcdir/$_gitname-build"

	python2 setup.py build
}

package() {
	cd "$srcdir/$_gitname-build"
	python2 setup.py install --root="${pkgdir}" --prefix=/usr

	# Copying the examples
	cp -R examples "${pkgdir}/usr/lib/python2.7/site-packages/pysfml"

	# Copying the License file
	install -D -m644 "$srcdir/$_gitname-build/LICENSE.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

	# Fixing permissions
	chmod 644 "${pkgdir}"/usr/lib/python2.7/site-packages/sfml.so
}
