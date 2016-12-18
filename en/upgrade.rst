=======
Upgrade
=======

Sonerezh does not provide automatic upgrades for the moment. We need to do it manually.

-------------------
0.9.0 to 1.0.0-beta
-------------------

.. warning:: Unfortunately it is not possible to upgrade Sonerezh from 0.9.0 to a more recent version. We have made too many deep changes between 0.9.0 and 1.0.0-beta and you need to install Sonerezh from scratch if you come from 0.9.0.

-------------------
1.0.0-beta to 1.0.0
-------------------

.. note:: You can use this section if you upgrade from the old 1.0.0-beta branch

^^^^^^^^
With git
^^^^^^^^
Get the last version from GitHub:

.. code-block:: sh

    cd /var/www/sonerezh
    git fetch
    git checkout tags/1.0.0

The dabatase schema has changed, you have to update it (php-cli required):

.. code-block:: sh

    # Follow the instructions given by the command
    app/Console/cake schema update sonerezh

You instance has been upgraded! You can verify it under the statistics, on the settings page. Do not forget to empty you browser cache and delete the Sonerezh cookies.

^^^^^^^^^^^
Without git
^^^^^^^^^^^
You cannot upgrade Sonerezh if you do not use git. You have to install the new version from scratch.

--------------
1.0.0 to 1.1.0
--------------

^^^^^^^^
With git
^^^^^^^^
Get the latest version from GitHub:

.. code-block:: sh

    $ cd /var/www/sonerezh
    /var/www/sonerezh $ git fetch
    /var/www/sonerezh $ git checkout tags/1.1.0

You instance is up to date! You can verify it under the statistics, on the settings page. Do not forget to empty you browser cache and delete the Sonerezh cookies.

^^^^^^^^^^^
Without git
^^^^^^^^^^^
There is not official procedure to update Sonerezh without Git. We advise you to make a fresh install with the latest archive. However, ``rsync`` should make the job:

.. code-block:: sh

    $ cd /var/www
    /var/www $ cp -a sonerezh sonerezh.backup
    /var/www $ wget https://github.com/Sonerezh/sonerezh/archive/1.1.0.tar.gz
    /var/www $ tar -zcf 1.1.0.tar.gz
    /var/www $ rsync -a sonerezh-1.1.0 sonerezh

--------------
1.1.0 to 1.1.1
--------------

^^^^^^^^
With git
^^^^^^^^
Get the latest version from GitHub:

.. code-block:: sh

    $ cd /var/www/sonerezh
    /var/www/sonerezh $ git fetch
    /var/www/sonerezh $ git checkout -b 1.1.1 tags/1.1.1

You instance is up to date! You can verify it under the statistics, on the settings page. Do not forget to empty you browser cache and delete the Sonerezh cookies.

^^^^^^^^^^^
Without git
^^^^^^^^^^^
There is not official procedure to update Sonerezh without Git. We advise you to make a fresh install with the latest archive. However, ``rsync`` should make the job:

.. code-block:: sh

    $ cd /var/www
    /var/www $ cp -a sonerezh sonerezh.backup
    /var/www $ wget https://github.com/Sonerezh/sonerezh/archive/1.1.1.tar.gz
    /var/www $ tar -zcf 1.1.1.tar.gz
    /var/www $ rsync -a sonerezh-1.1.1 sonerezh

--------------
1.1.1 to 1.1.3
--------------

^^^^^^^^
With git
^^^^^^^^
Get the latest version from GitHub:

.. code-block:: sh

    $ cd /var/www/sonerezh
    /var/www/sonerezh $ git fetch
    /var/www/sonerezh $ git checkout -b 1.1.3 tags/1.1.3

The dabatase schema has changed, you have to update it (php-cli required):

.. code-block:: sh

    # Follow the instructions given by the command
    # If you use MySQL
    app/Console/cake schema update sonerezhMysql

    # If you use PostreSQL
    app/Console/cake schema update sonerezhPgsql

You instance has been upgraded! You can verify it under the statistics, on the settings page. Do not forget to empty you browser cache and delete the Sonerezh cookies.

^^^^^^^^^^^
Without git
^^^^^^^^^^^
There is not official procedure to update Sonerezh without Git. We advise you to make a fresh install with the latest archive. However, ``rsync`` should make the job:

.. code-block:: sh

    $ cd /var/www
    /var/www $ cp -a sonerezh sonerezh.backup
    /var/www $ wget https://github.com/Sonerezh/sonerezh/archive/1.1.3.tar.gz
    /var/www $ tar -zcf 1.1.3.tar.gz
    /var/www $ rsync -a sonerezh-1.1.3 sonerezh

The dabatase schema has changed, you have to update it (php-cli required):

.. code-block:: sh

    # Follow the instructions given by the command
    # If you use MySQL
    app/Console/cake schema update sonerezhMysql

    # If you use PostreSQL
    app/Console/cake schema update sonerezhPgsql

You instance has been upgraded! You can verify it under the statistics, on the settings page. Do not forget to empty you browser cache and delete the Sonerezh cookies.
