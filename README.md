# mpd-sacd-archlinux
An update for [mpd-sacd@aur.archlinux.org](https://aur.archlinux.org/packages/mpd-sacd)
---

Thanks to [Maxim V. Anisiutkin](https://sourceforge.net/u/manisiutkin/profile/) and his outstanding work on the [Music Player Daemon SACD/DVD-A ISO decoder plugins](https://sourceforge.net/projects/mpd.sacddecoder.p/), listening to music from SACD ISO files on Linux is now possible.  

## Installation
1. Get all the files from Github.com
```bash
    git clone https://github.com/bruce-awareit/mpd-sacd-archlinux.git
```
2. cd the downloaded folder
```bash
    cd mpd-sacd-archlinux
```
3. <font color="red">If you don't need to listen to `Steam` audio, you can skip this step and proceed directly to the 4th step to install mpd-sacd.</font>

   In this `PKGBUILD`, the `vgmstream` option has been disabled. This option enables playback of `Steam` audio files.  
   If you need this functionality, please follow the steps below to enable it:

   * Install the `vgmstream-git` package from the AUR.  
   ```
   yay -S vgmstream-git
   ```

   * Edit the `PKGBUILD` file and delete the line that includes:  
   ```
   -D vgmstream=disabled
   ```

4. Make and Install the package
```bash
    makepkg -i  
```
