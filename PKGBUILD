# Maintainer: Christer Edwards <christer.edwards@gmail.com>
pkgname=salt-cloud-git
pkgver=20130410
pkgrel=2
pkgdesc="Salt Cloud is a generic cloud provisioning tool"
arch=('any')
url="https://github.com/saltstack/salt-cloud"
license=('APACHE')
groups=()
depends=('salt'
         'python2'
         'python2-yaml'
         'apache-libcloud'
         'python2-botocore')

makedepends=('git')
conflicts=('salt-cloud')
provides=('salt-cloud')

_gitroot="git://github.com/saltstack/salt-cloud.git"
_gitname="salt-cloud"

build() {
  cd ${srcdir}
  msg "Connecting to GIT server...."

  if [ -d ${_gitname} ] ; then
    cd ${_gitname} && git pull origin
    msg "The local files are updated."
  else
    git clone ${_gitroot} ${_gitname}
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf ${srcdir}/${_gitname}-build
  git clone ${srcdir}/${_gitname} ${srcdir}/${_gitname}-build

}

package() {
  cd ${srcdir}/${_gitname}-build
  export BOOTSTRAP_SCRIPT_VERSION=develop
  python2 setup.py sdist
  python2 setup.py install --root=${pkgdir}/ --optimize=1
}
