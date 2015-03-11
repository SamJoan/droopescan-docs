Scanning a few CMSs using droopescan
====================================

SilverStripe
------------

droopescan can be used at the moment to scan both silverstripe and drupal. It
ferrets out quite a bit of information about scanned websites, mainly version,
plugins and themes installed, as well as "interesting urls".

A super simple invocation for droopescan would be as follows::

    droopescan scan silverstripe -u http://localhost/full/silverstripe/

It only specifies the URL parameter (with `-u` or `--url`).

Please see the output for the line above, for SilverStripe. SilverStripe is a
very popular CMS in New Zealand::

    [+] Themes found:
        silverstrap http://localhost/full/silverstripe/themes/silverstrap/
            http://localhost/full/silverstripe/themes/silverstrap/README.md
        silverstrap-cerulean http://localhost/full/silverstripe/themes/silverstrap-cerulean/
            http://localhost/full/silverstripe/themes/silverstrap-cerulean/README.md

    [+] No interesting urls found.

    [+] Possible version(s):
        3.1.10
        3.1.10-rc1
        3.1.10-rc2

    [+] Plugins found:
        widgets http://localhost/full/silverstripe/widgets/
            http://localhost/full/silverstripe/widgets/README.md
            http://localhost/full/silverstripe/widgets/LICENSE
        sortablegridfield http://localhost/full/silverstripe/sortablegridfield/
            http://localhost/full/silverstripe/sortablegridfield/README.md
            http://localhost/full/silverstripe/sortablegridfield/LICENSE
        fulltextsearch http://localhost/full/silverstripe/fulltextsearch/
            http://localhost/full/silverstripe/fulltextsearch/README.md
            http://localhost/full/silverstripe/fulltextsearch/LICENSE
        userforms http://localhost/full/silverstripe/userforms/
            http://localhost/full/silverstripe/userforms/README.md
            http://localhost/full/silverstripe/userforms/LICENSE
        cms http://localhost/full/silverstripe/cms/
            http://localhost/full/silverstripe/cms/README.md

    [+] Scan finished (0:00:03.490551 elapsed)

Another interesting command-line parameter is `-e`, or `--enumerate`. With this
parameter, we can kindly ask droopescan to limit itself to a subset of it's
functionality. We could restrict it to version tests only, which aren't
intrusive (for a particular definition of intrusive which I invented)::

    droopescan scan silverstripe -u http://localhost/full/silverstripe/ -e v

In all seriousness, the test above makes seven requests, which would likely
happen in the course of regular browsing of the site::

    [+] Possible version(s):
        3.1.10
        3.1.10-rc1
        3.1.10-rc2

    [+] Scan finished (0:00:00.154158 elapsed)

More intrusive readers might want to make `droopescan` even more intrusive.
Parameters useful for such aggresive, aggro people are `--threads` and
`--number` (or `-t` and `-n` for short.)

These allow you to specify the number of threads you want to make use of, as
well as how many plugins to bruteforce for. Adding more threads makes scanning
generally faster, but it may turn out that your desktop overpowers the VPS the
CMS is installed on and you could get unreliable results (`droopescan` will
warn you with adorable "`Got a 500 error. Is the server overloaded?`" messages.)

Output can be controlled with the `--output` parameter.

Drupal
------

You might be suprised to read this, but `droopescan` can be used to scan
`Drupal` websites. It is after all, the reason the tool got its name. Here is
how you'd scan a drupal CMS running on your local server::

    droopescan scan drupal -u http://localhost/full/drupal/

Pretty simple. The output is as follows:

::

    [+] Themes found:
        adaptivetheme http://localhost/full/drupal/sites/all/themes/adaptivetheme/
            http://localhost/full/drupal/sites/all/themes/adaptivetheme/LICENSE.txt
        bootstrap http://localhost/full/drupal/sites/all/themes/bootstrap/
            http://localhost/full/drupal/sites/all/themes/bootstrap/README.txt
            http://localhost/full/drupal/sites/all/themes/bootstrap/LICENSE.txt

    [+] Possible interesting urls found:
        Default changelog file - http://localhost/full/drupal/CHANGELOG.txt

    [+] Possible version(s):
        7.34

    [+] Plugins found:
        views http://localhost/full/drupal/sites/all/modules/views/
            http://localhost/full/drupal/sites/all/modules/views/README.txt
            http://localhost/full/drupal/sites/all/modules/views/LICENSE.txt
        ctools http://localhost/full/drupal/sites/all/modules/ctools/
            http://localhost/full/drupal/sites/all/modules/ctools/CHANGELOG.txt
            http://localhost/full/drupal/sites/all/modules/ctools/LICENSE.txt
            http://localhost/full/drupal/sites/all/modules/ctools/API.txt
        google_analytics http://localhost/full/drupal/sites/all/modules/google_analytics/
            http://localhost/full/drupal/sites/all/modules/google_analytics/README.txt
            http://localhost/full/drupal/sites/all/modules/google_analytics/LICENSE.txt
        link http://localhost/full/drupal/sites/all/modules/link/
            http://localhost/full/drupal/sites/all/modules/link/LICENSE.txt
        backup_migrate http://localhost/full/drupal/sites/all/modules/backup_migrate/
            http://localhost/full/drupal/sites/all/modules/backup_migrate/README.txt
            http://localhost/full/drupal/sites/all/modules/backup_migrate/LICENSE.txt
        captcha http://localhost/full/drupal/sites/all/modules/captcha/
            http://localhost/full/drupal/sites/all/modules/captcha/README.txt
            http://localhost/full/drupal/sites/all/modules/captcha/LICENSE.txt
        realname http://localhost/full/drupal/sites/all/modules/realname/
            http://localhost/full/drupal/sites/all/modules/realname/README.txt
            http://localhost/full/drupal/sites/all/modules/realname/LICENSE.txt
        tagadelic http://localhost/full/drupal/sites/all/modules/tagadelic/
            http://localhost/full/drupal/sites/all/modules/tagadelic/LICENSE.txt

    [+] Scan finished (0:00:11.684791 elapsed)

To show off how accurate it is, I will run a `ls -la` of that drupal
installation and put the results here::

    root@debian-dev:~/droopescan# ls -la /var/www/html/full/drupal/sites/all/modules/
    total 44
    drwxr-xr-x 10 6226 6226 4096 Mar 11 17:52 .
    drwxr-xr-x  4 6226 6226 4096 Nov 19 15:24 ..
    drwxr-xr-x  3 root root 4096 Mar 11 17:52 backup_migrate
    drwxr-xr-x  3 root root 4096 Mar 11 17:52 captcha
    drwxr-xr-x 19 root root 4096 Mar 11 17:51 ctools
    drwxr-xr-x  2 root root 4096 Mar 11 17:52 google_analytics
    drwxr-xr-x  4 root root 4096 Mar 11 17:52 link
    -rw-r--r--  1 6226 6226  952 Nov 19 15:24 README.txt
    drwxr-xr-x  2 root root 4096 Mar 11 17:52 realname
    drwxr-xr-x  4 root root 4096 Mar 11 17:52 tagadelic
    drwxr-xr-x 14 root root 4096 Mar 11 17:51 views

Yeap, they are all there. Phew.

Mass-Scanning
-------------

You can use `droopescan` to scan multiple sites at the same time with the
`--url-file` or `-U` parameter (that's a capital U.) The URL file parameter
expects a path to a file which has a format like this::

    [...]
    http://localhost/drupal/7.22/
    http://localhost/drupal/7.23/
    http://localhost/drupal/7.24/
    http://localhost/drupal/7.25/
    http://localhost/drupal/7.26/
    http://localhost/drupal/7.27/
    http://localhost/drupal/7.28/
    http://localhost/drupal/7.29/
    http://localhost/drupal/7.3/
    http://localhost/drupal/7.30/
    http://localhost/drupal/7.31/
    http://localhost/drupal/7.32/
    http://localhost/drupal/7.33/
    http://localhost/drupal/7.34/
    http://localhost/drupal/7.4/
    http://localhost/drupal/7.5/
    http://localhost/drupal/7.6/
    http://localhost/drupal/7.7/
    http://localhost/drupal/7.8/
    http://localhost/drupal/7.9/
    http://localhost/drupal/8.0.0-beta1/
    http://localhost/drupal/8.0.0-beta2/
    http://localhost/drupal/8.0.0-beta3/
    http://localhost/drupal/8.0.0-beta4/
    http://localhost/drupal/8.0.0-beta5/
    http://localhost/drupal/8.0.0-beta6/
    [...]

Here's a sample run::

    /droopescan scan drupal -U /var/www/html/all_urls.txt -e v

The output, by default, is machine readable so you can use it in conjunction
with other scripts or parse it with awesome graph-generating tools.

::

    {"host": "http://localhost/drupal/7.22/", "version": {"is_empty": false, "finds": ["7.22"]}}
    {"host": "http://localhost/drupal/7.23/", "version": {"is_empty": false, "finds": ["7.23"]}}
    {"host": "http://localhost/drupal/7.24/", "version": {"is_empty": false, "finds": ["7.24"]}}
    {"host": "http://localhost/drupal/7.25/", "version": {"is_empty": false, "finds": ["7.25"]}}
    {"host": "http://localhost/drupal/7.26/", "version": {"is_empty": false, "finds": ["7.26"]}}
    {"host": "http://localhost/drupal/7.27/", "version": {"is_empty": false, "finds": ["7.27"]}}
    {"host": "http://localhost/drupal/7.28/", "version": {"is_empty": false, "finds": ["7.28"]}}
    {"host": "http://localhost/drupal/7.29/", "version": {"is_empty": false, "finds": ["7.29"]}}
    {"host": "http://localhost/drupal/7.3/", "version": {"is_empty": false, "finds": ["7.3"]}}
    {"host": "http://localhost/drupal/7.30/", "version": {"is_empty": false, "finds": ["7.30"]}}
    {"host": "http://localhost/drupal/7.31/", "version": {"is_empty": false, "finds": ["7.31"]}}
    {"host": "http://localhost/drupal/7.32/", "version": {"is_empty": false, "finds": ["7.32"]}}
    {"host": "http://localhost/drupal/7.33/", "version": {"is_empty": false, "finds": ["7.33"]}}
    {"host": "http://localhost/drupal/7.34/", "version": {"is_empty": false, "finds": ["7.34"]}}
    {"host": "http://localhost/drupal/7.4/", "version": {"is_empty": false, "finds": ["7.4"]}}
    {"host": "http://localhost/drupal/7.5/", "version": {"is_empty": false, "finds": ["7.2", "7.3", "7.4", "7.5"]}}
    {"host": "http://localhost/drupal/7.6/", "version": {"is_empty": false, "finds": ["7.6"]}}
    {"host": "http://localhost/drupal/7.7/", "version": {"is_empty": false, "finds": ["7.7"]}}
    {"host": "http://localhost/drupal/7.8/", "version": {"is_empty": false, "finds": ["7.8"]}}
    {"host": "http://localhost/drupal/7.9/", "version": {"is_empty": false, "finds": ["7.9"]}}
    {"host": "http://localhost/drupal/8.0.0-beta1/", "version": {"is_empty": false, "finds": ["8.0.0-alpha15", "8.0.0-beta1"]}}
    {"host": "http://localhost/drupal/8.0.0-beta2/", "version": {"is_empty": false, "finds": ["8.0.0-beta2"]}}
    {"host": "http://localhost/drupal/8.0.0-beta3/", "version": {"is_empty": false, "finds": ["8.0.0-beta3"]}}
    {"host": "http://localhost/drupal/8.0.0-beta4/", "version": {"is_empty": false, "finds": ["8.0.0-beta4"]}}
    {"host": "http://localhost/drupal/8.0.0-beta5/", "version": {"is_empty": false, "finds": ["8.0.0-beta5", "8.0.0-beta6"]}}
    {"host": "http://localhost/drupal/8.0.0-beta6/", "version": {"is_empty": false, "finds": ["8.0.0-beta5", "8.0.0-beta6"]}}

Some sample graphs can be seen in `a presentation I made`_ at OWASP NZ Day. The
topic is a mass-scan I ran of the whole of New Zealand.

Parameters of particular interest to mass-scanners are `--timeout-host`,
`--timeout` and `--error-log`. They all have sane defaults.

* `--timeout-host` specifies the maximum amount of time we are willing to spend
  on any particular host. Like NMAP's documentation states, "the slowest few
  percent of the scanned hosts can eat up a majority of the scan time".
* `--timeout` specifies how much to wait for any particular HTTP request.
* `--error-log` specifies where to store the errors. When mass-scanning, a lot
  of hosts fail because they are down, because hostnames don't resolve, and
  outputing those values to the console is just unbearably loud and un-helpful.
  `--error-log` allows you to pipe that into a file, which you can then inspect
  if you feel like it.

Output from this kind of scanning is stable. This means I won't break it on
purpose between `minor versions`_. It looks like this::

    {
      "themes": {
        "is_empty": true,
        "finds": [

        ]
      },
      "interesting urls": {
        "is_empty": false,
        "finds": [
          {
            "url": "https:\/\/www.drupal.org\/CHANGELOG.txt",
            "description": "Default changelog file."
          },
          {
            "url": "https:\/\/www.drupal.org\/user\/login",
            "description": "Default admin."
          }
        ]
      },
      "version": {
        "is_empty": false,
        "finds": [
          "7.29",
          "7.30",
          "7.31"
        ]
      },
      "plugins": {
        "is_empty": false,
        "finds": [
          {
            "url": "https:\/\/www.drupal.org\/sites\/all\/modules\/views\/",
            "name": "views"
          },
          [...snip...]
        ]
      }
    }

.. _a presentation I made: https://www.owasp.org/images/2/23/CMS_HELL.pptx
.. _minor versoins: http://semver.org/
