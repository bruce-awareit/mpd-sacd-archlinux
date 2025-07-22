# Maintainer: David Runge <dvzrv@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: T.J. Townsend <blakkheim@archlinux.org>
# Contributor: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>
# Contributor: Ben <ben@benmazer.net>
# Contributor: Foodle <bruce[at]mail.kh.edu.tw>

pkgname=mpd-sacd
programname=mpd
pkgver=0.25.0
pkgrel=2
pkgdesc="Flexible, powerful, server-side application for playing music"
arch=(x86_64 ARM64)
url="https://sourceforge.net/projects/mpd.sacddecoder.p/"
license=(
  BSD-2-Clause
  GPL-2.0-or-later
)
conflicts=('mpd')
provides=("mpd=${pkgver}")
depends=(
  gcc-libs
  glibc
  hicolor-icon-theme
  libcdio
  libcdio-paranoia
  libgme
  libmad
  libmms
  libmodplug
  libmpcdec
  # libnfs
  libshout
  libsidplayfp
  libsoxr
  # smbclient  # disabled because of https://bugzilla.samba.org/show_bug.cgi?id=11413
  pcre2
  wavpack
  wildmidi
  zlib
  zziplib
)
makedepends=(
  alsa-lib
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
  git
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
  sqlite
  systemd
  twolame
  # yajl
  nlohmann-json
)
backup=(etc/$programname.conf)
source=(
  $programname::git+https://git.code.sf.net/p/sacddecoder/mpd/MPD.git#commit=191ad0e58b9efba8757aed8f8c454ce5f6a9ab08
  $programname.conf
  $programname.sysusers
  $programname.tmpfiles
  $programname.service.override
)
sha512sums=('SKIP'
            '25a823740d92da8e186916701413114142eb6ad91a172c592e68b569c8e4f50fa99580e555ccf6cd31fc4f55a09bfe0278efa46e4e76ee0fe02846292fadf3c1'
            'd66c1d771160ee1781a05e57f383acc466babb29924c07d83ac0e763c14380dd1f279ba7b4aec508dc70245370d9732b4bc6287df1a2e06a920f3b73551d3032'
            'db473db27cd68994c3ee26e78e0fb34d13126301d8861563dcc12a22d62ecb14c4ffb1e0798c6aaccdff34e73bae3fbeeff7b42606c901a2d35e278865cdf35d'
            'c1782b82f9db1d30aece43a07230c5d57370f2494a16e108af03815d83968805472f10f53ea5495cf0e08ff8f245430c3c3bc44025af43aaf9ecd12fcd6afc6c')
b2sums=('SKIP'
        '0969a3c477b6a3f34b44e067e515d7f306414dd14e0163584417b9d071e3cc825898219f7ff66ead7905b15429b8411304052d3b2b14a72e560bfabf9bf0adcf'
        '814c2314de6040e895657a8c8d62f11bc38c224a3c0ef5cbf280c0e141c80f04b0ac5026be06fd5dc4a4b764f3d91ab46f365da0a7bd466abc3aed02b0612165'
        'd7b587c25dd5830c27af475a8fdd8102139d7c8fdd6f04fe23b36be030e4411582e289f575c299255ff8183096f7d47247327276f9a24641cbd032d9675b837a'
        '753664445d7d5cc0b36f51ac66549beea403b9731cbcb81b0a782974a0a73d90559ba93e6afcaa470b6f2f5a844c09ef695bdf3b1e6dfee97aa080f41b7fe513')
validpgpkeys=('0392335A78083894A4301C43236E8A58C6DB4512') # Max Kellermann <max@blarg.de>

build() {

  local _meson_options=(
    -D documentation=enabled
    -D chromaprint=enabled 
    -D sidplay=disabled # unclear why but disabled in the past
    -D adplug=disabled # not in an official repo
    -D audiofile=disabled 
    -D nfs=disabled # not need this option.
    -D sndio=disabled # interferes with detection of alsa devices
    -D shine=disabled # not in an official repo
    -D tremor=disabled # not in official repo
    -D iso9660=enabled
    -D libmpdclient=enabled
    -D pipe=true
    -D pulse=disabled
    -D pipewire=enabled
    -D qobuz=disabled # turn off this option.
    -D zzip=enabled
    -D b_ndebug=true
    -D sacdiso=true
    -D dvdaiso=false # turn off this options.
  )

  # NOTE: sndio conflicts with alsa
  # TODO: package adplug
  # TODO: package shine
  # env CC=clang CXX=clang++ arch-meson $programname build "${_meson_options[@]}" -D c_args="-std=c11" -D cpp_std=c++23
  arch-meson $programname build "${_meson_options[@]}" -D c_args="-std=c11" -D cpp_std=c++23
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  depends+=(
    alsa-lib libasound.so
    avahi libavahi-{client,common}.so
    bzip2 libbz2.so
    # chromaprint libchromaprint.so
    curl libcurl.so
    dbus libdbus-1.so
    expat libexpat.so
    faad2 libfaad.so
    ffmpeg libav{codec,filter,format,util}.so
    flac libFLAC.so
    fluidsynth libfluidsynth.so
    fmt libfmt.so
    icu libicui18n.so libicuuc.so
    jack libjack.so
    lame libmp3lame.so
    libao libao.so
    libid3tag libid3tag.so
    libmikmod libmikmod.so
    libmpdclient libmpdclient.so
    libogg libogg.so
    libopenmpt libopenmpt.so
    libpipewire libpipewire-0.3.so
    # libpulse libpulse.so
    libsamplerate libsamplerate.so
    libsndfile libsndfile.so
    libupnp libixml.so libupnp.so
    liburing liburing.so
    libvorbis libvorbis{,enc}.so
    mpg123 libmpg123.so
    openal libopenal.so
    opus libopus.so
    sqlite libsqlite3.so
    systemd-libs libsystemd.so
    twolame libtwolame.so
    # yajl libyajl.so
  )

  meson install -C build --destdir "$pkgdir"
  install -vDm 644 $programname/doc/${programname}conf.example -t "$pkgdir/usr/share/doc/$programname/"
  # NOTE: BSD-2-Clause license file currently missing: https://github.com/MusicPlayerDaemon/MPD/issues/1877
  # install -vDm 644 $programname-$pkgver/LICENSES/BSD-2-Clause -t "$pkgdir/usr/share/licenses/$programname/"
  install -vDm 644 $programname.service.override "$pkgdir/usr/lib/systemd/system/mpd.service.d/00-arch.conf"
  install -vDm 644 $programname.conf -t "$pkgdir/etc/"
  install -vDm 644 $programname.sysusers "$pkgdir/usr/lib/sysusers.d/$programname.conf"
  install -vDm 644 $programname.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$programname.conf"
}

# vim:set sw=2 sts-=1 et:
