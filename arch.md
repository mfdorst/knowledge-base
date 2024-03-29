# Archlinux

## View pacman logs
`/var/log/pacman.log` shows a log of every pacman operation, including each package that has been
updated, along with what version it was before. For example:
```
[2023-08-24T00:15:15-0700] [ALPM] upgraded git (2.41.0-2 -> 2.42.0-1)
```

## Roll back a specific package to a previously installed version
For a listing of all current and previous versions of installed packages
```
ls -l /var/cache/pacman/pkg
```
Let's say you want to revert to the previously installed version of Firefox.
```
.rw-r--r--  65M root  4 Aug 10:30 firefox-116.0.1-1-x86_64.pkg.tar.zst
.rw-r--r--  141 root  4 Aug 10:30 firefox-116.0.1-1-x86_64.pkg.tar.zst.sig
.rw-r--r--  65M root 16 Aug 18:02 firefox-116.0.3-1-x86_64.pkg.tar.zst
.rw-r--r--  141 root 16 Aug 18:02 firefox-116.0.3-1-x86_64.pkg.tar.zst.sig
```
We can see that on Aug 16th, Firefox was updated from `116.0.1-1` to `116.0.3-1`. To roll back, run
```
sudo pacman -U /var/cache/pacman/pkg/firefox-116.0.1-1-x86_64.pkg.tar.zst
```

## Roll back all packages to a previous date
Back up your mirror list
```
cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.old
```
Delete all entries in your mirrorlist, and replace them with the following:
```
Server=https://archive.archlinux.org/repos/<YYYY>/<MM>/<DD>/$repo/os/$arch
```
Do a full system downgrade
```
sudo pacman -Syyuu
```
Double `y` refreshes your package database, double `u` allows pacman to downgrade packages.

Make sure to `reboot` if you are downgrading the kernel or graphics drivers.

## Pin a package version
Say you have identified that the newest nvidia drivers are breaking your system. You have rolled
them back to working versions, but you would like to update the rest of your system. You can pin
their versions with `IgnorePkg` in `/etc/pacman.conf`.
```
IgnorePkg = nvidia nvidia-utils
```

## Check archlinux news before updating packages
Install `informant` from the AUR. It will create a pacman hook that stops you from upgrading until
you have read the latest news.

Run `sudo informant read` to read your unread archlinux news.

To enable reading informant news without `sudo`, run
```
sudo chown me /var/lib/informant.dat
```

## Install packages as a dependencies
```
pacman -S --asdeps <package1> <package2> ...
```

## View information about a package, including optional dependencies
```
pacman -Si <package>
```

## List files associated with a package
```
pacman -Ql <package>
```
