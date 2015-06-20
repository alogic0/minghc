# Minimum GHC Installer [![Build Status](https://img.shields.io/travis/fpco/minghc.svg?style=flat)](https://travis-ci.org/fpco/minghc)

This project provides a Windows installer with:

* [GHC](https://www.haskell.org/ghc/), so you can write Haskell code.
* [Cabal](https://www.haskell.org/cabal/), so you can install Haskell packages.
* [MSYS](http://www.mingw.org/wiki/MSYS), so packages with configure scripts (notably [network](https://hackage.haskell.org/package/network)) compile.

It _does not_ provide all the packages included with the [Haskell Platform](https://www.haskell.org/platform/), but it _does_ provide an environment where you can install those packages.  Some require [installing c libraries](docs/InstallingCLibs.md).


## Using the Installer

* [**Download installer with GHC 7.10.1 (32-bit)**](https://github.com/fpco/minghc/releases/download/2015-05-26/minghc-7.10.1-i386.exe)
* [**Download installer with GHC 7.10.1 (64-bit)**](https://github.com/fpco/minghc/releases/download/2015-05-26/minghc-7.10.1-x86_64.exe)
* [**Download installer with GHC 7.8.4 (32-bit)**](https://github.com/fpco/minghc/releases/download/2015-05-26/minghc-7.8.4-i386.exe)
* [**Download installer with GHC 7.8.4 (64-bit)**](https://github.com/fpco/minghc/releases/download/2015-05-26/minghc-7.8.4-x86_64.exe)

You may wish to also check the [Github latest releases page](https://github.com/fpco/minghc/releases/latest).

To use MinGHC, download and run the installer. There are two options you may wish to modify:

* "Add programs to PATH" - select this if you want to make this version of GHC the standard one you use for general development. It will modify your `%PATH%` environment variable so the MinGHC installed copies of `ghc` and `cabal` are used by default.
* "Add switcher to PATH" - select this if you want to use a different GHC normally, but occasionally switch to this version. After installation, type `minghc-7.8.3` at a command prompt to temporarily add the MinGHC copies of `ghc` and `cabal`.

_Caveats:_
* The `network` library doesn't work well with [Cygwin](https://cygwin.com/). Hence, it is not recommended that you use `cabal install` in a Cygwin terminal. Use Command Prompt (`cmd.exe`) or Windows PowerShell instead.

### Older installer links

* [GHC 7.6.3 (32-bit)](https://s3.amazonaws.com/download.fpcomplete.com/minghc/minghc-7.6.3.exe)
* [GHC 7.4.2 (32-bit)](https://s3.amazonaws.com/download.fpcomplete.com/minghc/minghc-7.4.2.exe)
* [GHC 7.2.2 (32-bit)](https://s3.amazonaws.com/download.fpcomplete.com/minghc/minghc-7.2.2.exe)

## Motivation

There are two existing ways to get GHC on Windows, straight from the [GHC distribution](https://www.haskell.org/ghc/) and using the [Haskell Platform](https://www.haskell.org/platform/). The GHC distribution is hard to unpack (`.xv` files are not Windows friendly), doesn't setup the `%PATH%`, lacks Cabal and cannot build the `network` library on its own. The Haskell Platform is easy to install and comes with more libraries, but still won't build the `network` library and usually lags the GHC release by months. This installer is the GHC distribution with all the issues above fixed.

## Building the Installer

Users of the installer have no need to build it, these are mostly notes for developers of the installer. To build one of the installers:

* Download [NSIS](http://nsis.sourceforge.net/) and put it on your `%PATH%`.
* Make sure you have copies of `tar`, `wget`, `bunzip`, `gzip`, and `7z` on your `%PATH%`. For `tar`, a version of BSD Tar is recommended.
    * For convenience, consider using the [minimal dependency bundle](https://s3.amazonaws.com/download.fpcomplete.com/minghc/minghcdeps-bin.zip), which includes all the necessary tools.
    * [GNU on Windows (GOW)](https://github.com/bmatzelle/gow) is a heavier option.
* Run `cabal install --only-dependencies`.
* Run `cabal run`. That will generate a file `.build/minghc-7.10.1.exe`.
* To build for other versions of GHC, pass the version on the command line, for example `cabal run -- 7.8.4`.
