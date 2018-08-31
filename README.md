ssb-pacman-git
===
> Secure-Scuttlebutt-based pacman back-end for reproducable installs

This repository containes sources of an Arch Linux (pacman) package, see [PKGBUILD](https://wiki.archlinux.org/index.php/PKGBUILD) for details. Being opinionated and special-purpose, it is not published on the AUR (Arch User Repository), but instead is part of a [collection of atomic configuration snippets](https://github.com/regaur) I use to build Arch-based systems.

Build
---

```
makepkg --sign
```

See Also
---

- [ssb-pacman](https://github.com/regular/ssb-pacman)
- [ssb-archiso](https://github.com/regular/ssb-archiso)
