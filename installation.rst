Installation Process
====================

An interested user may install droopescan utilizing pip.

::

    pip install droopescan

Some successful output looks as follows::

    user@host:~# pip install droopescan
    Downloading/unpacking droopescan
      Downloading droopescan-1.22.0.tar.gz (202Kb): 202Kb downloaded
      Running setup.py egg_info for package droopescan

    Requirement already satisfied (use --upgrade to upgrade): cement>=2.2,<2.2.99 in /usr/local/lib/python2.7/dist-packages (from droopescan)
    Requirement already satisfied (use --upgrade to upgrade): requests in /usr/local/lib/python2.7/dist-packages (from droopescan)
    Requirement already satisfied (use --upgrade to upgrade): pystache in /usr/local/lib/python2.7/dist-packages (from droopescan)
    Requirement already satisfied (use --upgrade to upgrade): futures in /usr/local/lib/python2.7/dist-packages (from droopescan)
    Installing collected packages: droopescan
      Running setup.py install for droopescan

        changing mode of build/scripts-2.7/droopescan from 644 to 755
        changing mode of /usr/local/bin/droopescan to 755
    Successfully installed droopescan
    Cleaning up...

Installation From Source
------------------------

Manual installation from source is also possible. droopescan is GPLv2 code.

::

    git clone https://github.com/droope/droopescan.git
    cd droopescan
    pip install -r requirements.txt
    ./droopescan scan --help 

In order to prevent unnecessary dependencies from being bundled with the final
binary, dependencies required for development are not included in the
`requirements.txt` file. Development dependencies can be installed with the
following commands::

    apt-get install python-dev libxslt1-dev libxml2-dev python3 zlib1g-dev python3-pip python3-dev
    pip install -r requirements_test.txt
    pip3 install -r requirements.txt -r requirements_test.txt

You can verify everything is in working order by running the automated tests::

    ./droopescan test
