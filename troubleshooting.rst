Common Issues
=============

It doesn't work!
----------------

It works on my machine! You can troubleshoot what's going on with the
`--debug-requests` parameter.

::

    root@localhost:~# droopescan scan drupal -u http://google.com/ -e v --debug-requests
    [head] http://google.com/ 301
    [get] http://www.google.com/misc/drupal.js 404 96c6ff5e1129a6535b2eb62362532546
    [get] http://www.google.com/misc/tabledrag.js 404 3616c53ebfd4c19e2ddc762bb0096cf1
    [get] http://www.google.com/misc/tableheader.js 404 4b1114a85b175cc12fbdda5c3dc4dbea
    [get] http://www.google.com/misc/ajax.js 404 7d24ea8067f75a44c0f3fd3fa6d4990d
    [get] http://www.google.com/core/misc/drupal.js 404 5fefb8249491a0bd86db72f0a36e757c
    [get] http://www.google.com/core/misc/tabledrag.js 404 8ad58022b53e714c049b3d6dd856de40
    [get] http://www.google.com/core/misc/tableheader.js 404 81b0f41b72dec22aebe6efa7e4284e03
    [get] http://www.google.com/core/misc/ajax.js 404 376f83a226b7c60e3e9288ee6afe6516
    [get] http://www.google.com/CHANGELOG.txt 404 70cbe47281305e66d03c7c601ecc9a2b
    [get] http://www.google.com/core/CHANGELOG.txt 404 c6571f0a56c603e3155ab85b689db76e

Based on the debug output, we can figure out that `droopescan` is asking for a
whole bunch of URLs and that google is saying those don't exist in that server.
It is likely that the server we are aiming `droopescan` at does not run drupal.

Outdated Requests Library
-------------------------

This issue manifests itself with the following error::

    Traceback (most recent call last):
      File "./droopescan", line 9, in <module>
        droopescan.main()
      File "/opt/droopescan/dscan/droopescan.py", line 45, in main
        ds.run()
      File "/usr/local/lib/python2.7/dist-packages/cement/core/foundation.py", line 520, in run
        self.controller._dispatch()
      File "/usr/local/lib/python2.7/dist-packages/cement/core/controller.py", line 455, in _dispatch
        func()
      File "/usr/local/lib/python2.7/dist-packages/cement/core/controller.py", line 461, in _dispatch
        func()
      File "/opt/droopescan/dscan/plugins/drupal.py", line 45, in drupal
        self.plugin_init()
      File "/opt/droopescan/dscan/plugins/internal/base_plugin_internal.py", line 215, in plugin_init
        self._general_init(output=output, debug_requests=debug_requests)
      File "/opt/droopescan/dscan/plugins/internal/base_plugin_internal.py", line 60, in _general_init
        a = requests.adapters.HTTPAdapter(pool_maxsize=5000)
    AttributeError: 'module' object has no attribute 'adapters'

If you've gotten this error, it is likely that it is because you are running an outdated version of requests (such as 0.12.1.)

The solution is to update it or to run droopescan in a virtualenv which has a more recent version, the aforemention can be achieved by executing the following command::

    pip install -U requests



