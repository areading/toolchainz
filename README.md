# toolchainz
Toolchainz is a GNU Toolchain builder for GNUde, bare-metal architectures. The resulting cross compiler runs on the build host and will generate executables for the specified target.

### About

A standard GNU toolchain consists of binutils, gcc, and gdb. Toolchainz will download the versions of these packages specified in the toolvers file, along with requisite supporting libraries (mpfr, gmp, and mpc), and build a cross-compiler for the desired target. The choice of target is (unsurprisingly) restricted to those supported by gcc.

Since the goal of toolchainz is to build for bare-metal targets, newlib is built and included with the resulting compiler, rather than the standard glibc. Native Language Support (NLS) is disabled.

The original scripts can be found at travisg/toolchains. They, however, do not integrate with newlib.

### Usage

There are two 'executor' scripts, buildit, and getit. They do exactly what the names suggest. getit is also capable of "ungetting" things and can be used as an analog to make clean.

The simplest, often fastest way to get up and running after cloning the repository is to have the script download all the necessary source files for you. Here, toolchainz will build a compiler for the Renesas RL78 architecture [-a rl78], fetch the files [-f], and build in parallel with two threads [-j 2]:

	./buildit -a rl78 -f -j 2

If no options are specified, some help is displayed.

The output directory can be moved to e.g. /opt/xxx-toolchain without issue: sysroot paths will be unaffected.

PATH can be modified by hand to include the new compiler, or, simply source the sourceme.env script to have this done for you. If the directory has been moved, then just let sourceme.env what it is:

	. sourceme.env /opt/xxx-toolchain

To clean up, just run

	./getit -c

### Specifics

The output compiler is built with C and C++ language support.

Newlib is compiled with nano malloc, C99 IO formats, no floating point IO, and no supplied syscalls.

All things have NLS support disabled.

