==============
Requirements
==============

-----------
Web server
-----------

Sonerezh is a web-based application which works with your browser. You need a web server to deploy it (Apache, Nginx...). You can find configuration samples for Apache and Nginx in the appendices, but we will not cover the web server installation.

.. note:: You need to enable the ``mod_rewrite`` module if you want to run Sonerezh with Apache. To enable it on Debian an derivative: ``sudo a2enmod rewrite && sudo service apache2 restart``.

---------------
Database
---------------

Sonerezh requires a MySQL or MariaDB database to sort your music. The database must be created and ready before the deployment.

1) Connect to the MySQL prompt:

.. code-block:: sh

    mysql -u root -p

2) Create the database, a database user and grant privileges:

.. code-block:: sql

    CREATE DATABASE sonerezh;
    GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY 'password';
    FLUSH PRIVILEGES;
    exit;

---
PHP
---

Sonerezh is cooked with CakePHP, and you need PHP to be installed.

* PHP >= 5.4
* PHP-GD PHP module

-----------------
Libav (optional)
-----------------

You need to install libav-tools if you want Sonerezh to convert your tracks to a readable format for your browser.

On Debian :

.. code-block:: sh

    sudo apt-get install libav-tools
