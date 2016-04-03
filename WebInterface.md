# Web Interface #

RAW CCTV Replay software is designed to be run as a service across a network. Once the software is [running](Running.md), the interface can be accessed via an internet browser on port 8080 of the host computer:
  * if accessing across a network, type _"http://raw-server:8080"_ into the browser address bar where "raw-server" is the name of the computer on which the software is running
  * if accessing on the same machine, type _"http://localhost:8080"_ into the browser address bar.

This will bring up the login screen.

![http://raw-cctv-replay.googlecode.com/files/raw_login_v1_0.jpg](http://raw-cctv-replay.googlecode.com/files/raw_login_v1_0.jpg)

Authentication for the username/password will be against that of the host computer or domain authentication if this has been set up.

## User levels ##

There are two user levels:
  * Normal user - can [view](Replay.md) attached hard disk drives;
  * Admin user - can [attach](Attaching.md) hard disk drives to RAW CCTV Replay, [view](Replay.md) and examine logs.