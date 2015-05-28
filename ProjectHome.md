Do you have a GSA and submit content to it via feeds?  Then this is for you!!!  The Feed Manager (FM) for the Google Search Appliance (GSA) is a MUST HAVE for anyone using feeds to submit data to the GSA.

The feed manager can perform the following tasks:
  * feedManager configuration via feedManager.cfg file
  * archiving of feeds
  * improved feed logging
  * threaded submission of feeds to one or more GSAs
  * feed validation (optional) and error reporting/logging
  * ability to modify a feed using an XSLT before it gets submitted
  * email notification on a per datasource basis
  * ability to configure a directory where feeds can be placed and picked up by the feed manager and then submitted (instead of submitting them to the feed manager using a port).
  * ability to accept either an XML sitemap file or a standard GSA XML feed file.
  * ability to configure one or more URLs where feeds/sitemaps can be retrieved from and then submitted.
  * ability to run the feed manager once, and then have it stop.  This will enable scheduling of the feed manager via cron/at jobs instead of having it stay alive and listening.
  * allow for a quick feed submission with no validation or XML parsing (needed for high volume population of GSAs or large feeds)

The following **requirements** must be met in order to use the GSA Feed Manager:
  * you must have a GSA (v4.6.4+)
  * you must have python v2.4+ or ActivePython 2.4+ installed on the machine where you will be installing the feed manager
  * in order to do the XML and feed validation, the lxml library must be installed for python.  You can find this library at http://codespeak.net/lxml/

TODO:
  * change where KeyboardInterrupt catch is so that it actually works as expected when the feed manager is listening on a socket.
  * add in whitelist and blacklist IP functionality
  * add in code to create directories that don't exist for both archiving and logging
  * add in log rotation
  * add in date based directories for archiving
  * make feeder multi-threaded
  * add ability to delete a feed by storing a deletion feed for every regular feed
  * add ability to compile single feeds into multiple feeds
  * add ability to split up large feeds into smaller groupings
  * allow the feed manager to split feeds based upon URL patterns and feed one or more GSAs
  * allow the feed manager to split feeds based upon meta data patterns and feed one or more GSAs

Please send suggestions and ideas to: fmackenz@gmail.com

For installation instructions, please see the GSA Feed Manager Installation document.