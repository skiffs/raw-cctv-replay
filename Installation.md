# Installation #

Once the source code has been [downloaded and built](Downloading.md), it needs to be installed. This page assumes that the built software resides in _~/raw_.

## Raw Configuration File ##

The RAW configuration file describes where you would like things in RAW to be installed on your machine, how RAW should authenticate itself, and various other parameters. An example configuration file is located at ~/raw/deploy/raw/etc/config-example.xml.

The parameters within this file that are most likely to be changed are:
  * _exclude-disk_ - disks that should be excluded for consideration by RAW CCTV Replay because they are system disks and do not contain CCTV data.
  * _user_ - the user who is to run RAW CCTV Replay software
  * _java-home_ - where java is located
Once this file has been edited, it should be saved somewhere sensible (_e.g. ~/raw\_config.xml_).

## Running the installer ##

The installer is located at _~/raw/intall/tools/bin/install\_raw_. This is a Python script that you run to give effect to your configuration parameters and to update your software installation. The location of your RAW installation is given in the configuration file.

You must run install\_raw as the user who is to run RAW; this means you may need to give that user access to the directory in which you want RAW installed.
To install or update a RAW installation, you can now just do:

> _$ ~/raw/install/tools/bin/install\_raw ~/raw\_config.xml ~/raw/_

which will:
  * Read your configuration file.
  * Install the software from ~/raw/deploy/raw to wherever the configuration file says it should live.
  * Write a setvars file in the target bin directory, overwriting any file prepared by the build.
  * Update rc.raw to point at this new setvars file.

Once this has been completed, RAW CCTV replay can then be [run](Running.md).