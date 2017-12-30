Download  or clone from:
	https://github.com/TALP-UPC/FreeLing

Follow instruntions from:
	https://github.com/TALP-UPC/FreeLing/blob/master/INSTALL

Version 2018-01-01 [modified by @sanxofon]:

-----------------------------------

## Installation Instructions

This file describes how to install FreeLing library from source.

Additional information about FreeLing, how to install and use it
can be found in FreeLing web page: http://nlp.lsi.upc.edu/freeling


If you are installing from source, you need to compile the library,
and that means you need some development tools and 3rd-party dependencies.

### You should have installed in your computer:

#### automake
 
check if you already have it:
  
  	automake --version

if you don't, install it:

	sudo apt install automake

#### autoconf
 
check if you already have it:
  
  	autoconf --version

if you don't, install it:

	sudo apt install autoconf

#### libtool
 
check if you already have it:
  
  	libtool --version

**if you don't have any of them, install by:**

	sudo apt install automake autoconf libtool-bin

#### g++  (or another C++ compiler)
 
check if you already have it:
  
  	g++ -v

if you don't, install it:

	sudo apt-get install g++

#### liboost
 
check version:
  
  	ldpkg -s libboost-dev | grep 'Version'

install it:

	sudo apt install libboost-dev libboost-filesystem1.58.0 libboost-iostreams1.58.0 libboost-program-options-dev libboost-program-options1.58-dev libboost-program-options1.58.0 libboost-random1.58.0 libboost-regex1.58.0 libboost-system1.58.0 libboost-thread1.58.0

or:

	sudo apt install libboost-filesystem1.58.0 libboost-iostreams1.58.0 libboost-program-options-dev libboost-program-options1.58-dev libboost-program-options1.58.0 libboost-random1.58.0 libboost-regex1.58.0 libboost-system1.58.0 libboost-thread1.58.0 libboost1.58-dev libboost1.58-tools-dev libboost-regex-dev libboost-regex1.58-dev libboost-system-dev libboost-system1.58-dev libboost-thread-dev libboost-thread1.58-dev


#### libicu
 
check version:
  
  	dpkg -s libicu-dev | grep 'Version'

install it:

	sudo apt install libicu55 libicu-dev

#### zlib
 
check if you already have it:
  
  	zlib --version

if you don't, install it:

	sudo apt install zlib1g zlib1g-dev 


More details on how to install these dependencies in FreeLing user manual.

Once the tools and libraries are installed, you need to do.

  autoreconf --install
  ./configure
  make
  make install

These four steps should be used regardless of how did you obtain your source
(either from a .tag.gz source package or from a git clone)

Read below for some hints and additional options you can use with these commands
to speed up compilation or to save disk space.


* First step (autoreconf) will create necessary configuration files to enable
customization to your particular OS.

* Second step (configure) will check that all dependencies are present and
create required Makefiles to compile the library in your system.
  "configure" accepts several options (see "./configure --help" for details)
though the most used is "--prefix=/some/path" that specifies where you want
to install FreeLing (if prefix is not specified, the library will be
installed in /usr/local).

* Third step (make) will compile the library.  This will take some time, so
you can go for a coffee meanwhile.
  If you have a multicore machine, you can speed up the compilation by
using the option "-j" for "make".
  E.g. "make -j 4" will use 4 cores and thus compile 4 times faster.
  Note that even if you have many cores, using too many of them will also
use a lot of RAM and migth freeze you OS. A good rule of thumb is using
as many cores as Gb of RAM your machine has.

* Last step (make install) will install the library in its final location
(/usr/local, or the chosen --prefix, if any).
  If you don't have writting permision for the destination directory (as is
the case for /usr/local) this command must be executed as root (or with 'sudo').
  Once installed, you can remove your source directory if you don't want/need
 to keep it.
  Also, this command will install language data in /usr/local/share/freeling
(or the choosen --prefix, if any). Folders for unneeded languages can be
safely removed to save disk space.

*************************
Installation with the FreeLing ASR system based on Kaldi
*************************

By default, FreeLing's ASR (Automatic Speech Recognition) system is not
installed, because its data is too big to download with the project.
To install the ASR module, follow this steps:

1. Download or clone Kaldi from its github webpage:
  "https://github.com/kaldi-asr/kaldi"

2. Compile Kaldi as a shared library, following the instructions in
  the INSTALL file in the root directory of Kaldi.
   You'll need to follow the instructions there that desribe how to
  use OpenFST-1.4 

3. Install FreeLing with this commands:
  autoreconf --install
  ./configure --with-kaldi-asr=/KALDI/INSTALLATION/DIR
  make
  make install


* Make sure you have an active internet connection, since the make install
command will download and install the ASR system data from the FreeLing webpage.

### For python API install

Install python-dev:

	sudo apt install python3-dev

Install swig:

	sudo apt install swig

Issue 'make' to compile the python API

	make