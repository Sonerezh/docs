============
Installation
============

No headhaches with complicated configuration files. You just have to download and uncompress the archive.

----------------------------------
Installation on a dedicated server
----------------------------------

As Sonerezh does not have auto-updater yet, we recommend you to use Git to download the sources, it will facilitate the update process.

.. note:: We will install Sonerezh in ``/var/www/sonerezh``, and make it reachable to http://demo.sonerezh.bzh.

Install Sonerezh with Git:

.. code-block:: sh

    cd /var/www
    sudo git clone --branch master https://github.com/Sonerezh/sonerezh.git
    sudo chown -R www-data: sonerezh/ && sudo chmod -R 775 sonerezh/

But if you prefer, you can also download a ZIP archive from GitHub.

.. code-block:: sh

    cd /var/www
    sudo wget https://github.com/Sonerezh/sonerezh/archive/1.0.0-beta.zip
    sudo unzip 1.0.0-beta.zip
    sudo mv sonerezh-1.0.0-beta sonerezh
    sudo chown -R www-data: sonerezh && sudo chmod -R 775 sonerezh

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
2) Download Sonerezh from GitHub_
3) Upload and decompress the archive on your distant hosting, for example in ``sonerezh/``
4) Go to the installation page (for example http://demo.sonerezh.bzh/install)
5) Fill in the form
6) Enjoy your music :)


------------------------------------------
Installation example on Ubuntu Server
------------------------------------------
This is an example to install Sonerezh on Ubuntu Server 14.10 (Apache 2.4, PHP 5.5 and MySQL 14.14). In this example, 
the default installation path is ``/var/www/html/sonerezh`` and it is deployed on http://www.myserver.com/sonerezh.

^^^^^^^^^^^^^^^^^
Download Sonerezh
^^^^^^^^^^^^^^^^^
As mentioned above, it is recommended to use Git to download the sources (install it with ``sudo apt-get install git``):

.. code-block:: sh

    cd /var/www/html/
    sudo git clone --branch master http://github.com/Sonerezh/sonerezh.git
    sudo chown -R www-data: sonerezh/ && sudo chmod -R 775 sonerezh/

^^^^^^^^^^^^^^^^^^^
Create the database
^^^^^^^^^^^^^^^^^^^
1) Connect to the MySQL prompt:

.. code-block:: sh

    mysql -u root -p

2) Create the database, a database user and grant privileges:

.. code-block:: sql

    CREATE DATABASE sonerezh;
    GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY 'yourpassword';
    FLUSH PRIVILEGES;
    exit;

^^^^^^^^^^^^^^^^^^^^^^^^^
Configure your web server
^^^^^^^^^^^^^^^^^^^^^^^^^
Make sure ``mod_rewrite`` is enabled:

.. code-block:: sh

    sudo a2enmod rewrite

Edit your config file:

.. code-block:: sh

    sudo vim /etc/apache2/sites-available/sonerezh.conf

Then add your site:

.. code-block:: apache

    <VirtualHost *:80>
        ServerName      www.myserver.com
        DocumentRoot    /var/www/html/sonerezh
    
        <Directory /var/www/html/sonerezh>
            Options -Indexes
            AllowOverride All
            <IfModule mod_authz_core.c>
                Require all granted
            </IfModule>
        </Directory>
        
        CustomLog   /var/log/apache2/www.myserver.com-access.log "Combined"
        ErrorLog    /var/log/apache2/www.myserver.com-error.log
    </VirtualHost>

Save the file, enable the new virtual host and restart your web server:

.. code-block:: sh

    sudo a2ensite sonerezh && sudo service apache2 restart
    
^^^^^^^^^^^^^^^^^^
Configure Sonerezh
^^^^^^^^^^^^^^^^^^
In your browser, go to http://www.myserver.com/sonerezh and fill in the form with your parameters. Enjoy your music!

.. _GitHub: https://github.com/Sonerezh/sonerezh/archive/1.0.0-beta.zip
