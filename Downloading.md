# Download Source Code and Building #

## Requirements ##

You'll need Ubuntu 10.10 or above, ideally.

You'll also need to install :

> _$ sudo apt-get install git_

And you'll need a JDK. You can get the default one with:

> _$ sudo apt-get install openjdk-6-jdk_

But you can equally well download the Oracle JDK from java.sun.com and use that. You'll want to set:

> _$ export JAVA\_HOME=/usr/lib/jvm/default-java_

(or wherever you installed your JDK of choice).

The build process for RAW CCTV Replay makes use of a build system called  [Muddle](http://http://code.google.com/p/muddle/)
The source code for RAW CCTV Replay can then be downloaded either [via muddle](Downloading#Download_via_muddle.md) or [via a tar ball](Downloading#Download_via_tar_ball.md). Once the source code has been downloaded, it must be [built](Downloading#build.md) via muddle.

## Installing muddle ##


To get muddle:


> _$ cd /opt_

> _$ sudo git clone https://code.google.com/p/muddle/_

> _$ export PATH=$PATH:/opt/muddle_


## Download source code muddle ##

Once muddle is installed, the source code for RAW CCTV Replay can be downloaded:

> _$ mkdir ~/raw_

> $ cd ~/raw

> $ muddle init git+https://code.google.com/p/raw-cctv-replay builds/01.py

> _$ muddle checkout `_`all_

## Download via tar ball ##

A tar ball of the source code can be found [here](http://code.google.com/p/raw-cctv-replay/downloads/list). Once downloaded, extract via:

> _$ tar xvf raw-cctv-replay-vX.Y.tgz_

where _X.Y_ is the version of the software downloaded.

## Build ##

With the source code for RAW CCTV Replay downloaded, it is build via Muddle. Make sure you are in the correct folder (_i.e_ the folder in which you either did the Muddle checkout or the extracted folder from the tar ball).


> _$ muddle_

After installing the packages it needs (be sure to hang around to answer 'Yes' when it asks), this will build the system itself. This may take some time!

Once it is built, RAW CCTV Replay software can then be [installed](Installation.md).