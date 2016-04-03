# Running #

Once the software is [download, built](DownloadSourceCodeAndBuilding.md) and [installed](Installation.md) the following command:

> _$ /opt/raw/bin/rc.raw start_

will start everything up and

> _$ /opt/raw/bin/rc.raw stop_

to shut it down.

If you want this to happen automatically on startup or shutdown, symlink _/opt/raw/bin/rc.raw_ into the relevant directory (usually _/etc/rc2.d/_ ). rc.raw just su's to the user specified in the setvars script and then calls down to rawctl - rawctl must be run as a mortal.