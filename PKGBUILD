# Maintainer: Aaron Fischer <mail@aaron-fischer.net>

pkgname=dataexplorer
pkgver=3.4.6
pkgrel=2
pkgdesc="Graphical tool to analyze data, gathered from various hardware devices."
url="http://savannah.nongnu.org/projects/dataexplorer"
arch=("i686" "x86_64")
license=("GPL3")
install=$pkgname.install
makedepends=("apache-ant" "jdk8-openjdk")
depends=("java-runtime")
source=("http://download.savannah.gnu.org/releases/dataexplorer/dataexplorer-$pkgver-src.tar.gz"
        "http://download.savannah.gnu.org/releases/dataexplorer/dataexplorer-$pkgver-src.tar.gz.sig"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-FTDI.rules"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-FTDI.rules.sig"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-MosChip.rules"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-MosChip.rules.sig"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-ProfilicTechnology.rules"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-ProfilicTechnology.rules.sig"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-SiliconLabs.rules"
        "http://download.savannah.gnu.org/releases/dataexplorer/udev_rules/40-SiliconLabs.rules.sig")
noextract=("dataexplorer-$pkgver-src.tar.gz.sig"
           "40-FTDI.rules"
           "40-FTDI.rules.sig"
           "40-MosChip.rules"
           "40-MosChip.rules.sig"
           "40-ProfilicTechnology.rules"
           "40-ProfilicTechnology.rules.sig"
           "40-SiliconLabs.rules"
           "40-SiliconLabs.rules.sig")
sha512sums=('2b109a9cbc9fbc3426d8902257986d42c1ffc7fb918edd7da1fabaaeebf0c221b5c64fdc15c2291a6bbbf74dbf1b9708ee7db8f56e75dec21d28ba8237e6bf96'
            '91748be539dcf05ee659f27ed93564ab84ce36ecbccad909977bc0c41609a12db034629ca1c14ca4c4513561027c51c4168b458cf4494db5a70c9669aa09bdc1'
            'adc0d042c68970d21c3e44faa29015e6d916a14587ea73c2273e7b15351d161d4d54ccc94293a67e53d63d97a70e0dbee6a2b5af30e6e1f8df6f12cb27516036'
            '92464b35e56f438aec2fe616e8cb42476f29bea40849d8fcbddb6d5d455ad67a5d2efb9e37b58d0951b9971b0d6b77f3fc6a1332a194ac46d6244cc1da84cbc5'
            '8bb9d77e86e47a5a42bfdf661ea35a4543b3a22336ae4f718657e12089091cf1d6664fd1090e194da4c56f34c5febef960f50692246a1109ded19921854b9e5f'
            '51ca93b5d37ac76fb2a58996a982f9cf897dcd03d3bdc547eb59145bf0a5c47e8a48c3f937fe734404d292866c7e4efe6c932bfc490cced7c58284ab17d25a39'
            '3174d20d0de4b8cf0756b1fe69563ca4c3133b108bdda2bd90a8b0163d3f35c826c1356544735181023f2cbaee71a3a7224f88221ad57fa187a52c4d04fe023a'
            'c35f332fe0adf297b7fcdccf3d4b8fdf535895c18afd4b9e47276c9a51f29de38884d0d8831f9794237a3e1fd3de2c2103c76e75d6834e2b270e609b0e6f1bed'
            '8d969524ae67b5170976efd408ab4c28b23d8a33bc0d671d1b968a6cab4ebfbc80067561f1837470c8cd92e711df136851fec85e683ddf7fd1a33f93b6e39210'
            '886c2d0f809134c6f3e7787ca2c044fce838fb09dd4cfdd19af2ce2122fd8e4177f6424f849c18ca417b7581f96e47c264e445471bf4069f065d8045a6c08fc3')
validpgpkeys=("3F0CC709ECF91C5CC0BE9E601D295C19C9C06AF6") # Winfried Bruegmann

build() {
  echo $pkgdir

  cd "$srcdir/$pkgname-$pkgver"

  if [ ! -e "RXTXcomm" ]; then
    ln -s "thirdparty/rxtx-2.2pre2" "RXTXcomm"
  fi

  ./configure --prefix=$pkgdir/opt
  make

  cd "$srcdir"
  echo -e "#!/usr/bin/env sh\ncd /opt/DataExplorer && ./DataExplorer" > "dataexplorer.sh"
  echo -e "#!/usr/bin/env sh\ncd /opt/DataExplorer && ./DevicePropertiesEditor" > "deviceproperties-editor.sh"
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  mkdir "$pkgdir/opt"
  make install

  install -Dm755 "$srcdir/dataexplorer.sh" "$pkgdir/usr/bin/dataexplorer"
  install -Dm755 "$srcdir/deviceproperties-editor.sh" "$pkgdir/usr/bin/deviceproperties-editor"

  install -Dm644 "$srcdir/40-FTDI.rules" "$pkgdir/etc/udev/rules.d/40-FTDI.rules"
  install -Dm644 "$srcdir/40-MosChip.rules" "$pkgdir/etc/udev/rules.d/40-MosChip.rules"
  install -Dm644 "$srcdir/40-ProfilicTechnology.rules" "$pkgdir/etc/udev/rules.d/40-ProfilicTechnology.rules"
  install -Dm644 "$srcdir/40-SiliconLabs.rules" "$pkgdir/etc/udev/rules.d/40-SiliconLabs.rules"

  install -Dm644 "$pkgdir/opt/DataExplorer/DataExplorer.desktop" "$pkgdir/usr/share/applications/DataExplorer.desktop"
  install -Dm644 "$pkgdir/opt/DataExplorer/DevicePropertiesEditor.desktop" "$pkgdir/usr/share/applications/DevicePropertiesEditor.desktop"
  install -Dm644 "$pkgdir/opt/DataExplorer/DataExplorer.xpm" "$pkgdir/usr/share/pixmaps/DataExplorer.xpm"
  install -Dm644 "$pkgdir/opt/DataExplorer/DevicePropertiesEditor.xpm" "$pkgdir/usr/share/pixmaps/DevicePropertiesEditor.xpm"
  rm "$pkgdir/opt/DataExplorer/DataExplorer.desktop"
  rm "$pkgdir/opt/DataExplorer/DevicePropertiesEditor.desktop"
  rm "$pkgdir/opt/DataExplorer/DataExplorer.xpm"
  rm "$pkgdir/opt/DataExplorer/DevicePropertiesEditor.xpm"

  chmod +x "$pkgdir/opt/DataExplorer/DataExplorer"
  chmod +x "$pkgdir/opt/DataExplorer/DevicePropertiesEditor"
}
