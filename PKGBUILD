# Maintainer: Atom Long <atom.long@hotmail.com>

_realname=go
pkgname=${_realname}-bin
pkgver=1.20.5
pkgrel=1
pkgdesc="Core compiler tools for the Go programming language"
replaces=(go)
provides=(go)
conflicts=(go)
url="https://go.dev/"
license=('BSD')
options=(!strip staticlibs)
arch=('i686' 'x86_64')
source_i686=("https://go.dev/dl/go${pkgver}.windows-386.zip")
source_x86_64=("https://go.dev/dl/go${pkgver}.windows-amd64.zip")
sha256sums_i686=('af6655ad9eff15baebb738b7b416f0f67037b1cd03036bfa4e8aede393fb7c44')
sha256sums_x86_64=('c04a4ed73c3624d5b4c4f62e44a141549cc0bfd83a7492c31ca8b86b3752f077')
install="${pkgname}.install"

prepare() {
export MSYS="winsymlinks:native"
}

package() {
  cd "${_realname}"

  mkdir -p "${pkgdir}${MSYSTEM_PREFIX}/"{bin,lib/go,lib/go/doc,lib/go/src,lib/go/site/src,share/licenses/go,share/doc/go,share/go}

  mkdir -p "${pkgdir}${MSYSTEM_PREFIX}/share/licenses/go"
  install -Dm644 "${srcdir}"/${_realname}/LICENSE \
    "${pkgdir}${MSYSTEM_PREFIX}/share/licenses/go/LICENSE"

  cp -rf bin pkg src lib misc api test "${pkgdir}${MSYSTEM_PREFIX}/lib/go"
  cp -r doc/* "$pkgdir/${MSYSTEM_PREFIX}/share/doc/go"
  
  ln -sf ${MSYSTEM_PREFIX}/lib/go/bin/go "$pkgdir/${MSYSTEM_PREFIX}/bin/go"
  ln -sf ${MSYSTEM_PREFIX}/lib/go/bin/gofmt "$pkgdir/${MSYSTEM_PREFIX}/bin/gofmt"
  ln -sf ${MSYSTEM_PREFIX}/share/doc/go "$pkgdir/${MSYSTEM_PREFIX}/lib/go/doc"
  
  install -Dm644 VERSION "${pkgdir}${MSYSTEM_PREFIX}/lib/go/VERSION"
  install -Dm644 LICENSE "${pkgdir}${MSYSTEM_PREFIX}/share/licenses/go/LICENSE"
 
  # install profile script 
  mkdir -p "${pkgdir}"/etc/profile.d
  echo "export GOROOT=${MSYSTEM_PREFIX}/lib/go" > "${pkgdir}"/etc/profile.d/go.sh
  cp "${pkgdir}"/etc/profile.d/go.{sh,zsh}
}

