# Introduction #

This page contains the installation instructions for the GSA Feed Manager v1.3. All the appropriate files can be found in the zip file that is available in the downloads section.


# Details #

### Requirements ###

  * one or more GSAs v4.6.4+
  * python v2.4+ or ActivePython v2.4+ must be installed on the machine where you will be installing the feed manager
  * in order to do the XML and feed validation, the lxml python library must be installed. You can find this library at: http://codespeak.net/lxml/

## Installation Instructions ##

==> NOTE: Google does not warranty or in any way guarantee the reliability of this code. Use it at your own risk.

==>NOTE: Before starting, it is important to make sure that you meet the requirements for the feed manager


### Download and UnZip Feed Manager ###

Unzip the file feedManager\_v1.3.zip file where you want to have the feed
manager run.  This will create the appropriate directory, and all the default
locations for the archives and logs.


### Configure Feed Manager ###

Configure the feed manager by editing the feedManager.cfg file.

In the general section, enter in the feedmethod.  Valid values for feedmethod
are server, directory, or url.  Each feed method has its own configuration
section which describes the method in more detail.  Enter the feedtype, with
feed or sitemap, depending on the type of documents that will be send to the
feed manager.  Configure the feedthrottle using an integer number.  In general,
this will be a low number, unless you have very large feeds and you want to
pause between each feed in order to give the GSA some time between each feed
submission to process the feed.  If you wish to only run the feed manager once,
in directory or URL mode only, you can set the feedonce directive to True.
Otherwise, set it to False.  For example:

```
[general]
# Valid feed types are server, directory, or url
# feedertype:directory
feedmethod:server
# Valid feed types are feed or sitemap
feedtype:sitemap
# How long to rest the feeder between runs when it is not in feed once mode
feedthrottle:2
# If feedonce is true, then the feed manager will only run once and quit.
feedonce:True
```


In the server section, enter in the host and port that the feed manager will
be running on.  You can either enter in localhost, 127.0.0.1, or the actual
IP of the machine.  Lastly you will need to configure the
serverfeedersleeptime.  This determines just how long the feeder will sleep
between checks for new feeds.  I would suggest between 1 and 10 seconds for
the serverfeedersleeptime.  For example:

```
# This is only used if the feed type is server.
[server]
# The host that the feed manager is running on.
host:localhost
# The port that the feed manager is running on.
port:19900
# The amount of time to wait between each check on the socket (in seconds)
serverfeedersleeptime:1
```


In the url section, enter in the number of URLs that will be used to feed
and the URLs themselves by using the number and url properties as shown
below.  The last setting will be the urlfeedersleeptime which determines
just how long the feeder will sleep between gathering all the URLs.
For example:

```
# This is only used if the feed type is URL.
[url]
# The number of URLs to read from
number:2
# The URL(s) for the feeds/sitemaps
url1:http://host.domain.com/sitemap.php
url2:http://host2.domain.com/sitemap.php
# The amount of time to wait between each pull of the url (in seconds)
urlfeedersleeptime:86400
```


In the directory section, enter in the directory that the feed manager will
watch, using the filefeederdir configuration option.  You will also have to
put in the filefeederextension and the filefeedersleep time.  The
filefeedersleeptime defines the amount of time that the directory watcher
waits between checking for new files to appear in the filefeederdir.
For example:

```
# This is only used if the feed type is directory.
[directory]
# The directory to watch for new feeds
filefeederdir:c:\feedmanager\feeds\
# The extension of the files that are feeds in the feeds directory
filefeederextension:.xml
# The amount of time to wait between each poll of a directory (in seconds)
filefeedersleeptime:60
```


In the logger section, put in the path to the directory where the logs will
be stored, the name of the main logfile, and the extension of the log files.
For example:

```
[logger]
# The directory that the feed manager logs will be stored in.
logdir:c:\feedmanager\logs\
# The name of the logfile (excluding the extension)
logname:feedManager
# The extension of the log file
logext:.log
```


In the archiver section, put in the path to the directory where the archive
files will be stored.  For example:

```
[archiver]
# The directory that feeds will be archived to.
archivedir:c:\feedmanager\archives\
```


In the validator section, put in the path to the feed.dtd file which will
be used to validate the feed xml files that are sent to the feed manager.
For example:

```
[validator]
# Do we want the feed manager to validate feeds being submitted.
# Note: Feed validation SEROIUSLY affects the speed of feed submission.
validate:False
# The location of the feed.dtd that will be used to validate the XML feeds.
feeddtd:c:\feedmanager\feed.dtd
```


In the notifier section, enter in the from email address, whether the SMTP
server requires a SSL connection, whether the SMTP server requires
authentication, the SMTP server host and port.  If the SMTP server requires
authentication, you will need to enter in the username and password to
authenticate to the SMTP server.  For example:

```
[notifier]
# Do we need authentication to send the email.  In the case of GMAIL, this
# must be set to True. Valid values are: True or False
smtpauth:True
# Email notifications will be sent as this user.
fromemail:gsa_feed_manager@gmail.com
# Do we require SSL to send the emails.  In the case of GMAIL, this
# must be set to True.  For other cases, it may be set to True or False
# depending on your email provider.  Valid values are: True or False
smtpssl:True
# The server hostname which will be used for the SMTP connection.
smtpserverhost:smtp.gmail.com
# The server port which will be used for the SMTP connection.
smtpserverport:587
# The username used for the authentication to the SMTP server.
authuser:gsa_feed_manager@gmail.com
# The password used for the authentication to the SMTP server.
authpassword:gsa_feed_managerspassword
```

or

```
[notifier]
smtpauth:True
fromemail:someuser@yourcorp.com
smtpssl:False
smtpserverhost:smtp.yourcorp.com
smtpserverport:25
authuser:someuser
authpassword:someuserspassword
```


For each data source that will be fed into the feed manager, you will
require a section in the feed manager.  For example, if the data source
name was feedsource1, then the section name in the configuration file would
be feedsource1 (see below).

If you wish to perform a transformation on the feed that is received, before
it is submitted, set the value of transformFeed to True and set transformXSL
to the full path and filename to the XSLT that will be used to transform the
feed.  Please note, that similarly to the feed validation, the feed
transformation significantly slows down the speed of the feed manager when
working with large feeds.

For sending email notifications to a user when a feed is submitted (both
successfully and unsuccessfully), you must set notifyuser to True and
put in a valid email address for the person to be notified.

Set the value of number to the number of GSAs that you will be submitting
the feed two.  In the example below, the number is 2 as we are submitting
the feed to two different GSAs.  You must also set the destinationhost# and
destinationport# for each host that you will be submitting a feed to.  Please
note that # is the actual number of the host in the configuration file
(see example below).

```
[feedsource1]
transformFeed:False
transformXSL:c:\feedmanager\feed.xsl
notifyuser:True
toEmail:someuser@yourcorp.com
number:2
destinationhost1:somehost1.yourdomain.com
destinationport1:19900
destinationhost2:somehost2.yourdomain.com
destinationport2:19900
```


Sitemaps, when they are converted to a feed, will always have a datasource name
of web.  Therefore, there is a required data source section of web, if you're
using the sitemap feeder functionality.

If you wish to perform a transformation on the feed that is received, before
it is submitted, set the value of transformFeed to True and set transformXSL
to the full path and filename to the XSLT that will be used to transform the
feed.  Please note, that similarly to the feed validation, the feed
transformation significantly slows down the speed of the feed manager when
working with large feeds.

For sending email notifications to a user when a feed is submitted (both
successfully and unsuccessfully), you must set notifyuser to True and
put in a valid email address for the person to be notified.

Set the value of number to the number of GSAs that you will be submitting
the feed two.  In the example below, the number is 2 as we are submitting
the feed to two different GSAs.  You must also set the destinationhost# and
destinationport# for each host that you will be submitting a feed to.  Please
note that # is the actual number of the host in the configuration file
(see example below).

```
[web]
# Does this feed need to be transformed before it is sent to the GSA(s).
# Valid values are: True or False
transformFeed:False
# The xsl file that will be used to transform the feed
transformXSL:c:\feedmanager\feed.xsl
# Should an email notification be sent out.  Valid values are: True or False
notifyuser:False
# What email address should the email notification be sent out to?
toEmail:someuser@yourcorp.com
# The number of GSAs to send the feed to.
number:1
# The hostname of GSA 1 that the feed is to be sent to
destinationhost1:somehost1.yourdomain.com
# The port of GSA 1 that the feed connection is made on
destinationport1:19900
```



### Modify Feed Manager Program ###

Modify the feedManager.py file, to change the first line to point to your
instance of python.  This needs to be done, as it defines which instance of
python you will be using.  This is especially important if you have more
than one version of python installed on the machine where the feed manager
will be running.

For example, if you use ActivePython v2.5 and it is installed in the c:
directory then you would change the line to:

```
#!c:\Python25\python25.exe
```

If you use python on unix/linux, and the executable is in /usr/bin, then you
would change the line to:

```
#!/usr/bin/python
```


### Starting Up the Feed Manager ###

Starting up the feed manager is as easy as typing in:

```
./feedManager.py
```

It can also be started by specifying python (you may have to specify the full
path to python if it isn't in your current path) in front of it as so:

```
python feedManager.py
```

You can make sure that the feed manager is running, by looking at the feed
manager log file, as defined in the feed manager configuration.