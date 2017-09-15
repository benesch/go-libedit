# go-libedit 

Go wrapper around `libedit`, a replacement to GNU readline using the BSD license.

![travis](https://travis-ci.org/knz/go-libedit.svg?branch=master)

**Prerequisites: ncurses/terminfo development headers.**

How to use:

- `go build` / `go install`
- see `test/example.go` for a demo.
- basic idea: call `Initialize()` once. Then call `SetPrompt()` and
  `Readline()` as needed. Finally call `Cleanup()`.

## How to force using the system-wide libedit on GNU/Linux

By default, the **go-libedit** package uses the bundled `libedit`
sources on GNU/Linux, so that `go get` works out of the box.

To force the package to use a system-wide libedit instead, edit `edit.go` as follows:

- remove the line containing `#cgo linux CFLAGS`
- change the line containing `#cgo linux CPPFLAGS` to read: `#cgo linux CPPFLAGS: -I/usr/include/editline -Ishim`
- change the line containing `#cgo linux LDFLAGS` to read: `#cgo linux LDFLAGS: -ledit`

## How to refresh the bundled libedit sources

(Only needed when upgrading the bundled `libedit` to a newer version.)

This procedure should be ran on a Debian/Ubuntu system.

1. ensure that `/etc/apt/sources.list` contains source repositories, i.e. the `deb-src`  lines are uncommented. Run `apt-get update` as necessary.
2. run:

   ```
   $ sudo apt-get install libbsd libbsd-dev libncurses-dev`
   $ cd src
   $ bash refresh.sh
   ```
