Humdrum Toolkit for Music Research
==================================

This repository contains the "classical" Humdrum Toolkit.
To use along with the [Humdrum Extras](https://github.com/craigsapp/humextra) 
package, it is better to install the Humdrum Toolkit from:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;https://github.com/humdrum-tools/humdrum-tools 

The Humdrum Toolkit is a set of [unix
command-line](https://www.youtube.com/watch?v=bE9DyH43C2I) programs
which process data files, including musical scores, in the Humdrum
file format.  The Humdrum Toolkit can used on unix-based computer
systems such as linux and Apple OS X.  To use in MS Windows, install
a unix terminal emulator.  A comprehensive package for linux tools
in Windows can be downloaded from http://www.cygwin.com.  The
simplest method is to download all cygwin packages when installing,
but that will require a long installation duration (such as overnight
for some reason).

If you are lucky or a unix expert (and have git and gcc installed),
then you can run the following commands to download and install the
Humdrum Toolkit as a single-user installation as well as download
sample musical data and test all of the tools (some commands may need
to be prefixed with ```sudo```):
```bash
   cd /usr/local
   git clone https://github.com/humdrum-tools/humdrum
   cd humdrum
   make bin
   make install
   make data
   make regression
```
Otherwise, follow the more detailed instructions below.

Further documentation about the Humdrum Toolkit as well 
as installing and using it can be found at http://www.humdrum.org.


Downloading
===============================

To download the Humdrum Toolkit package, go to the following page 
on the GitHub website:
  https://github.com/humdrum-tools/humdrum
and then click on the "Download ZIP" button.

However, the preferable method of downloading the Humdrum Toolkit
is with the [git](http://git-scm.com) command. If you have git installed
on your computer (see below for git installation notes), download the 
Humdrum Toolkit repository with the command:
```bash
    cd /usr/local    # recommended installation location
    git clone https://github.com/humdrum-tools/humdrum
    # or if there are permission writing errors, try:
    sudo git clone https://github.com/humdrum-tools/humdrum
```

To use alongside the [Humdrum Extras](https://github.com/craigsapp/humextra) 
package, instead download the
[humdrum-tools repository](https://github.com/humdrum-tools/humdrum-tools) 
by typing:
```bash
    cd /usr/local
    git clone --recursive https://github.com/humdrum-tools/humdrum-tools
```

If you want to download sample Humdrum file musical scores but not the 
Humdrum Extras package, you can do this command in the main Humdrum Toolkit
directory after downloading (if you have git installed):
```bash
   cd humdrum
   make data
```

Or to use the humdrum-data repository outside of the humdrum directory, type
the following command within the target installation directory:
```bash
    git clone --recursive https://github.com/humdrum-tools/humdrum-data
```

### installing git ###

[Git](http://git-scm.com/book/en/Getting-Started-Git-Basics) is a
version control program that is the main interface to online
repositories on GitHub.  To check if the ```git``` program is
installed on your computer, type:
```bash
   which git
```
If the terminal replies with a line such as ```/usr/local/bin/git```,
then git is installed and you can run the above installation commands.
If the ```which``` command replies with an error that git cannot
be found, you need to install git.  How to do this will depend on
your operating system.  

In linux, the installation command for git is usually one of these two 
possibilities:
```bash
   sudo yum install git
   sudo apt-get install git
```

For [cygwin](http://www.cygwin.com) on MS Windows computers, you
should have included ```git``` when installing packages when you
first installed cygwin.  Re-run the installation program and include
git in the package installation list.

For Apple OS X, the easiest method is to download git from [this
link](http://git-scm.com/download/mac).  More advanced Mac users
can use [Homebrew](http://brew.sh) to install git:
```bash
   brew install git
```


Compiling 
=========

To compile the C programs and create the ```bin``` directory for the
Humdrum Toolkit, type ```make bin``` inside of the humdrum directory:
```bash
    cd humdrum
    make bin
```
Also, typing just ```make``` will give a list of things you can
do with the make command, listed in the order that they can be done.

Note that to use the ```make``` command or ```gcc``` for compiling
the C programs, these must already be installed.  Check to see if
gcc is installed by typing this command (gcc installation includes
make command as well):
````bash
   which gcc
   which make
```
The terminal should reply with something like ```/usr/bin/gcc```
and ```/usr/bin/make```.  If gcc is not installed, then you will
have to figure out how to install it on your computer first.
Linux/Unix computers usually have it pre-installed with the operating
system; if not, then typing ```sudo yum install gcc``` or ```sudo
apt-get install gcc``` will typically install it.  Apple OS X does
not include it by default, so you will have to install it.  If you
are using OS X Mavericks or later, then type ```xcode-select
--install``` to install the Xcode command line tools. The ```make```
command will be installed at the same time that ```gcc``` is
installed.  Cygwin users would have to re-run the installation
program and include the compile tools if gcc was not initially
installed with cygwin.


Installing
==========

To use the Humdrum Toolkit commands within any directory, you must add the
humdrum/bin directory to the PATH environmental variable.  This can be
done temporarily for the current session by typing:
```bash
    cd humdrum  # or cd /usr/local/humdrum or wherever it is installed
    PATH=`pwd`/bin:$PATH
```

For a persistent installation of the Humdrum Toolkit whenever you
open a new terminal, you can type the following command to include
the humdrum/bin directory in the PATH command search path variable
within the file ~/.profile.
```bash
   make install
```
This installation method is suitable for single-user installations.
Super-users can instead install for all users on a computer system by
running this command:
```bash
   sudo echo "export PATH=/usr/local/humdrum/bin:$PATH" >> /etc/profile"
```
if /usr/local/humdrum is the directory where the Humdrum Toolkit was
downloaded to.


Verifying
=========

Once the Humdrum Toolkit has been installed, check that the humdrum/bin
directory has been added correctly to the PATH environmental variable by typing:
```bash
   echo $PATH | tr : '\n' | grep humdrum | head -n 1
```
which should display the humdrum/bin directory for the Humdrum Toolkit.
If the above command produces no result, see the previous section about adding
humdrum/bin to the PATH variable.  You can further check that the commands
are visible by running the ```which``` command:
```bash
	which mint
```
This should reply with the location of the mint command, 
such as ```/usr/local/humdrum/bin/mint```.

Further testing can be done to ensure that the Humdrum Toolkit
commands are performing as expected on your particular computer
system.  Within the main Humdrum Toolkit directory (such as
/usr/local/humdrum), type ```make regression```.   This will run
all of the Humdrum Toolkit programs with various inputs and compare
to expected outputs.  The start of the test sequence should look
something like this:

```bash
   (cd toolkit-source/regression-tests; make -s verbose)
   TEST 01 for accent: OK
   TEST 01 for assemble: OK
   TEST 01 for barks: OK
   TEST 01 for cbr: OK
   TEST 01 for census: OK
   TEST 01 for cents: OK
   TEST 01 for cleave: OK
   TEST 01 for cocho: OK
   TEST 01 for context: OK
   TEST 01 for correl: OK
   TEST 01 for deg: OK
   TEST 01 for degree: OK
   TEST 01 for ditto: OK
```


Updating
========

To periodically update the humdrum package if you downloaded 
using <em>git</em>, type these commands in the installation directory 
for humdrum (make commands may need to be prefixed with ```sudo``):
```bash
   cd /usr/local/humdrum
   make update
   make bin
```



