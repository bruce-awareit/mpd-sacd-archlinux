# mpd-sacd-archlinux
An update for [mpd-sacd@aur.archlinux.org](https://aur.archlinux.org/packages/mpd-sacd)
---

Thanks to [Maxim V. Anisiutkin](https://sourceforge.net/u/manisiutkin/profile/) and his outstanding work on the [Music Player Daemon SACD/DVD-A ISO decoder plugins](https://sourceforge.net/projects/mpd.sacddecoder.p/), listening to music from SACD ISO files on Linux is now possible.  

There are quick and dirty patches for fmt ver. 11.1.2-1 and libnfs ver. 6.0.2-3 on Arch Linux.  
Please refer to Issues of [MusicPlayerDaemon on GitHub](https://github.com/MusicPlayerDaemon/MPD)

1. [Failed compile with libfmt-11.1.0 #2173](https://github.com/MusicPlayerDaemon/MPD/issues/2173)
2. [about libnfs api v2 change #2165](https://github.com/MusicPlayerDaemon/MPD/issues/2165)



## Installation
1. Get all the files from Github.com
```bash
    git clone https://github.com/bruce-awareit/mpd-sacd-archlinux.git
```
2. cd the downloaded folder
```bash
    cd mpd-sacd-archlinux
```
3. Make and Install the package
```bash
    makepkg -i  
```
