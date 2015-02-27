============
Installation
============

No headhaches with complicated configuration files. You just have to download and uncompress the archive.

----------------------------------
Installation on a dedicated server
----------------------------------

As Sonerezh does not have auto-updater yet, we recommend you to use Git to download the sources, it will facilitate the update process.

.. note:: We are installing Sonerezh in ``/var/www/sonerezh``, an deploying it to http://demo.sonerezh.bzh.

But if you prefer, you can also download a ZIP archive on GitHub.

Install Sonerezh with Git:

.. code-block:: sh

    cd /var/www
    sudo git clone https://github.com/Sonerezh/sonerezh.git
    sudo chown -R wwww-data: sonerezh/ && sudo chmod -R 775 sonerezh/

Install Sonerezh with the zip archive:

.. code-block:: sh

    cd /var/www
    sudo wget https://github.com/Sonerezh/sonerezh/archive/master.zip
    sudo unzip master.zip
    sudo chown -R www-data: sonerezh-master/ && sudo chmod -R 775 sonerezh-master/

^^^^^^^^^^^^^^^^^^^^^^^^
Preparing the web server
^^^^^^^^^^^^^^^^^^^^^^^^

Several configuration samples are available in the :doc:`annexes`

^^^^^^^^^^^^^^^^^^^^^^^^^
Deploying the application
^^^^^^^^^^^^^^^^^^^^^^^^^

That's all ! You just have to go to http://demo.sonerezh.bzh/install and fill in the form to provide database connection informations.

------------------------------
Installation on shared hosting
------------------------------

The installation process on shared hosting is almost the same than on dedicated server. 

1) Prepare your database, depending on your hosting provider
2) Download Sonerezh on `GitHub`
3) Upload and decompress the archive on your FTP, for example in ``sonerezh/``
4) Go to the installation page (for example http://demo.sonerezh.bzh/install)
5) Fill in the form
6) Enjoy your music :)

.. _GitHub: https://github.com/Sonerezh/sonerezh/archive/master.zip
