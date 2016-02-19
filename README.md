Flightgear Build Script
=======================

Introduction
------------

This is a simple build script for building minimal Flightgear from source. It 
does not deal with the initial cloning of source from a remote repository and it
compiles flightgear, simgear, openscenegraph and terragear.

It is specifically designed for users who want to build Flightgear for
debugging purposes. You should install all the prerequisites tools and 
libraries for building Flightgear before running this script. You will need
the libgoogle-perftools-dev package because linking is done against the malloc
from that library.

The script has been tested on Ubuntu 15.04. This is beta software and
you should only use it if you understand what it does.

Usage
-----

<pre>
fgbuild [OPTIONS]

 -c        cleans the build directories before building
 -d DATE   build from DATE (YYYYMMDD)
 -g        build with debug symbols
 -j N      builds with N parallel jobs
 -l        builds with address sanitizer for leak checking
 -u        update from current state of next (not compatible with -d)
 -h        show usage message
 -H        show detailed usage message
</pre>

If the -j option is not supplied, the build will run with as many threads as
you have processors or cores.

Note that options that involve updating from a remote repository (-u and -d)
will checkout the next branch in your flightgear, simgear and fgdata 
directories. If you were working on another branch, they will not check it 
back out, or attempt to rebase your changes.

Examples
--------

A typical build to update from the latest sources (flightgear + simgear):

<pre>
$ fgbuild -u
fgbuild: 08:10:42: Updating from remote
fgbuild: 08:10:46: Building simgear
fgbuild: 08:10:59: Building flightgear
fgbuild: 08:11:13: Build complete
</pre>

The output from the build goes into $FG_SRC/fgbuild.log.

To update from the latest sources and compile everything from scratch:

<pre>
$ fgbuild -cu
</pre>

To clean and build with debug symbols (to run with gdb for crash reporting):

<pre>
$ fgbuild -cg
</pre>

To clean and build Flightgear as it existed on a given date (for bisection):

<pre>
$ fgbuild -cd 20141231
$ fgbuild -cd 'Dec 31 2014'
</pre>

To build with address sanitizer for checking leaks and debug symbols:

<pre>
$ fgbuild -clg
</pre>

