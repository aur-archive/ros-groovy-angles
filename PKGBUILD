pkgdesc="ROS - math utilities for working with angles."
url='http://www.ros.org/'

pkgname='ros-groovy-angles'
pkgver='1.9.8'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-catkin)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/angles ]; then
    cd ${srcdir}/angles
    git fetch origin --tags
    git reset --hard release/groovy/angles/${pkgver}-0
  else
    git clone -b release/groovy/angles/${pkgver}-0 git://github.com/ros-gbp/geometry_angles_utils-release.git ${srcdir}/angles
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/angles
  cmake ${srcdir}/angles -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
