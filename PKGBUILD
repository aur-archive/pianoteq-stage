# Maintainer: Simon Thorpe <simon@hivetechnology.com.au>
pkgname=pianoteq-stage
pkgver=5.2.1
pkgrel=1
pkgdesc="Piano library using physical modelling synthesis. Both standalone and VSTi versions."
arch=('i686' 'x86_64')
url="https://www.pianoteq.com/pianoteq5"
license=('commercial')
makedepends=('gendesk' 'wget' 'p7zip')
source=('http://www.macupdate.com/images/icons128/30550.png')
sha256sums=('9a6e68ef215f6704716443f656930212f5e99accc4beae4678802c01097ef608')

_filename=pianoteq_stage_linux_trial_v521.7z
_sha256sum=7d0dc5482339d74e8e877ada35d23a0386e216670a4d0a657b984444e2b02f07

prepare(){
  # Download the 7z file. URL changes daily so must scrape parent page.
  URL="https://www.pianoteq.com/$(wget https://www.pianoteq.com/try?file=$_filename -qO-|grep noscript|grep -oE 'try\?q=[a-zA-Z0-9]*')"
  wget --content-disposition "$URL"
  echo $_sha256sum $_filename|sha256sum -c || { echo 'Checksum failed!'; exit 1; }
  7z x $_filename
  
  gendesk -n --pkgname "$pkgname" --pkgdesc "$pkgdesc" \
    --name='Pianotek STAGE' \
    --categories 'Audio;Sequencer;Midi;AudioVideoEditing;Music;AudioVideo;'
}

package(){
  mkdir -p $pkgdir/usr/local/bin
  mkdir -p $pkgdir/usr/lib/vst
  if [[ "$CARCH" == i686 ]]; then
    install -Dm755 "$srcdir/Pianoteq 5 STAGE/i386/Pianoteq 5 STAGE" "$pkgdir/usr/local/bin/pianoteq-stage"
    install -Dm755 "$srcdir/Pianoteq 5 STAGE/i386/Pianoteq 5 STAGE.so" "$pkgdir/usr/lib/vst/Pianoteq 5 STAGE.so"
  else
    install -Dm755 "$srcdir/Pianoteq 5 STAGE/amd64/Pianoteq 5 STAGE" "$pkgdir/usr/local/bin/pianoteq-stage"
    install -Dm755 "$srcdir/Pianoteq 5 STAGE/amd64/Pianoteq 5 STAGE.so" "$pkgdir/usr/lib/vst/Pianoteq 5 STAGE.so"
  fi
  install -Dm644 "$srcdir/30550.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
  install -Dm644 "$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
}
