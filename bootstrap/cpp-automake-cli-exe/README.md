# Simple Autoconf "hello world."
This is a super simple autoconf that implements only the
bare essentials necessary to compile a c++ application.

### Quick Start:

```bash
$ autoreconf --install
$ ./configure
$ make
$ src/hello
hello world.
$ make distcheck
```