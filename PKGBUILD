# Maintainer: Bruce-AwareIT <bruce@awareit>

pkgname=mpd-sacd
srcfilename=mpd
pkgver=0.23.13
pkgrel=1
pkgdesc='MPD with patches for SACD and DVDA ISO playback.'
url='https://sourceforge.net/p/sacddecoder/mpd/MPD.git/ci/master/tree/'
license=('GPL')
arch=('i686' 'x86_64' 'aarch64' 'armv7h')
depends=(
  gcc-libs
  glibc
  libcdio
  libcdio-paranoia
  libgcrypt
  libgme
  libmad
  libmms
  libmodplug
  libmpcdec
  libnfs
  libshout
  libsidplayfp
  libsoxr
  # smbclient  # disabled because of https://bugzilla.samba.org/show_bug.cgi?id=11413
  wavpack
  wildmidi
  zlib
  zziplib
)
makedepends=(
  alsa-lib
  audiofile
  avahi
  boost
  bzip2
  chromaprint
  curl
  dbus
  expat
  faad2
  ffmpeg
  flac
  fluidsynth
  fmt
  icu
  jack
  lame
  libao
  libid3tag
  libmikmod
  libmpdclient
  libogg
  libopenmpt
  libpulse
  libsamplerate
  libsndfile
  libupnp
  liburing
  libvorbis
  meson
  mpg123
  openal
  opus
  libpipewire
  python-sphinx
  python-sphinxcontrib-jquery
  python-sphinx_rtd_theme
  sqlite
  systemd
  twolame
  yajl
)
conflicts=('mpd')
provides=("mpd=${pkgver}")
source=(
  $srcfilename.zip
  $srcfilename.conf
  $srcfilename.sysusers
  $srcfilename.tmpfiles
  $srcfilename.service.override
  $srcfilename.patch
)
sha512sums=(
            '73e30fbb6f9a1414d174f8b5c596d0386e11d2f202df97a3f09cb2a95095b3001d01bcaf03c9db087beac0cbdf6e51aa8f85f5905b667af8b7c3cbd44e1ff287'
            '25a823740d92da8e186916701413114142eb6ad91a172c592e68b569c8e4f50fa99580e555ccf6cd31fc4f55a09bfe0278efa46e4e76ee0fe02846292fadf3c1'
            '6e467481406279767b709ec6d5c06dbd825c0de09045c52ffa2d21d0604dcfe19b7a92bf42bed25163d66a3a0d1dbde6185a648b433eaf5eac56be90491e2e18'
            'db473db27cd68994c3ee26e78e0fb34d13126301d8861563dcc12a22d62ecb14c4ffb1e0798c6aaccdff34e73bae3fbeeff7b42606c901a2d35e278865cdf35d'
            'c1782b82f9db1d30aece43a07230c5d57370f2494a16e108af03815d83968805472f10f53ea5495cf0e08ff8f245430c3c3bc44025af43aaf9ecd12fcd6afc6c'
            'b9b546788675238a126d1f8b0331911d59bef10a196989656ab3356d79a5bf6612a30a62a73cdc6f0f6d30757da9acb9dfd5e15a43cd1f8b859be9ec18536cd3')
backup=('etc/mpd.conf')

prepare() {
	cd "${srcdir}/mpd"
	patch --forward --strip=1 --input="${srcdir}/../mpd.patch"
	install -d build
}

build() {
	cd "${srcdir}/mpd/build"
	_opts=('-Ddocumentation=enabled'
		'-Dchromaprint=disabled' # appears not to be used for anything
		'-Dsidplay=disabled' # unclear why but disabled in the past
		'-Dadplug=disabled' # not in an official repo
		'-Dsndio=disabled' # interferes with detection of alsa devices
		'-Dshine=disabled' # not in an official repo
		'-Dtremor=disabled' # not in official repo
		'-Dcdio_paranoia=enabled'
		'-Diso9660=enabled'
		'-Djack=enabled'
		'-Dlibmpdclient=enabled'
		'-Dpipe=true'
		'-Dpulse=enabled'
		'-Dsoundcloud=enabled'
		'-Dzzip=enabled'
		'-Dsacdiso=true'
		'-Ddvdaiso=true'
	)
	env CC=clang CXX=clang++ arch-meson .. ${_opts[@]}
	ninja
}

check() {
  ninja -C mpd/build test
}

package() {

DESTDIR="$pkgdir" ninja -C mpd/build install
  install -vDm 644 ${srcdir}/$srcfilename/doc/${srcfilename}conf.example -t "$pkgdir/usr/share/doc/$pkgname/"
  install -vDm 644 $srcfilename.service.override "$pkgdir/usr/lib/systemd/system/mpd.service.d/00-arch.conf"
  install -vDm 644 $srcfilename.conf -t "$pkgdir/etc/"
  install -vDm 644 $srcfilename.sysusers "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
  install -vDm 644 $srcfilename.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
}
