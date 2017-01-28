=============
Configuration
=============
All Sonerezh's settings can be found on the ``/settings`` page. This page also shows some statistics about your library, or the storage space used by the caches.

--------------------
Music root directory
--------------------
Here you can specify the absolute path of the folder in which sonerezh must look for your music.

.. tip:: Make sure Sonerezh can read this folder recursively.
.. warning:: We strongly recommend you to **NOT** store your music in the application folders (app/ and its subfolders).

-------------------------
Enable mail notifications
-------------------------
Sonerezh can send email to new users, or allow them to retrieve a forgotten password. Make sure PHP can send emails before enable this option.

Similar to database configuration, email configuration can be centralized in a class called ``EmailConfig``, in ``app/Config/email.php``. The ``app/Config/email.php.default`` has an example for this file.

You can follow the `official CakePHP documentation <http://book.cakephp.org/2.0/en/core-utility-libraries/email.html>`_ to configure the different transport methods to send email. The following configuration should work in most cases (if you already have a MTA available).

.. code-block:: php

    <?php
    class EmailConfig {
        public $default = array(
            'transport' => 'Mail',
            'from' => 'no-reply@sonerezh.bzh',
            'charset' => 'utf-8',
            'headerCharset' => 'utf-8',
        );
    } 

In this example, Sonerezh will send email using the PHP function ``mail()``.

---------------------------
Automatic tracks conversion
---------------------------
If your library contains tracks which can not be read by your browser, Sonerezh can convert them to OGG/Vorbis or MP3.

.. tip:: Sonerezh needs the ``avconv`` command to convert the tracks. It requires ``libav-tools``.

-------------------
Database management
-------------------
The settings page allows you to make some maintenance operations on Sonerezh, its database and its cache:

* Database update: run the import process. Usefull if you recently added new songs;
* Clear the cache : empty the cache (converted tracks and resized covers);
* Reset the database : reset the database. All songs and playlists **WILL BE LOST**. Don't panic, Sonerezh will never modify or delete your files.

----------
Statistics
----------
You can find some statistics about Sonerezh:

* Artists quantity (correspond to ``band`` tag)
* Albums quantity
* Tracks quantity
* Thumbnails cache size (the resized covers stored in ``app/webroot/img/resized/``
* Songs cache (the converted tracks stored in ``app/tmp/*.{ogg,mp3}``
