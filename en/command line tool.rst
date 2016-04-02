=================
Command line tool
=================

Since version 1.1.0, Sonerezh offers a command line tool which allows you to process collections with a lot of tracks. This tool is built on the `CakePHP Shell <http://book.cakephp.org/2.0/en/console-and-shells.html>`_ and can be used as below.

.. code-block:: sh

    $ cd /var/www/sonerezh/app
    /var/www/sonerezh/app $ Console/cake sonerezh import [OPTIONS] <path>

-------------------------
Import songs with the CLI
-------------------------

With the cli, you will be able to import an individual audio file:

.. code-block:: sh

    /var/www/sonerezh/app $ Console/cake sonerezh import /home/guillaume/Music/file.mp3
    Welcome to CakePHP v2.8.1 Console
    ---------------------------------------------------------------
    App : app
    Path: /var/www/sonerezh/app/
    ---------------------------------------------------------------
    [INFO] You asked to import /home/guillaume/Music/file.mp3. Continue? (yes/no)
    [yes] >
    [INFO] Run import: [100%] [#############################################]

If the path is a directory, Sonerezh will scan its content:

.. code-block:: sh

    /var/www/sonerezh/app $ Console/cake sonerezh import /home/guillaume/Music/album-folder
    Welcome to CakePHP v2.8.1 Console
    ---------------------------------------------------------------
    App : app
    Path: /var/www/sonerezh/app/
    ---------------------------------------------------------------
    [INFO] Scan /home/guillaume/Music/album-folder...
    [INFO] Found 13 audio files (0 already in the database). Continue? (yes/no)
    [yes] >
    [INFO] Run import: [100%] [#############################################]

Or you can also ask Sonerezh to scan a folder tree, with the ``-r``, or ``--recursive`` option:

.. code-block:: sh

    /var/www/sonerezh/app $ Console/cake sonerezh import -r /home/guillaume/Music
    Welcome to CakePHP v2.8.1 Console
    ---------------------------------------------------------------
    App : app
    Path: /var/www/sonerezh/app/
    ---------------------------------------------------------------
    [INFO] Scan /home/guillaume/Music...
    [INFO] Found 614 audio files (13 already in the database). Continue? (yes/no)
    [yes] >
    [INFO] Run import: [100%] [#############################################]

Your collection should be available on the web interface :)
