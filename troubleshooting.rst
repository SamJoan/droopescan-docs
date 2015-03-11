Common Issues
=============

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



