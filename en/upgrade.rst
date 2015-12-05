=======
Upgrade
=======

Sonerezh does not provide automatic upgrades for the moment. We need to do it manually.

------------------
Upgrade from 0.9.0
------------------

.. warning:: Unfortunately it is not possible to upgrade Sonerezh from 0.9.0 to a more recent version. We have made too many deep changes between 0.9.0 and 1.0.0-beta and you need to install Sonerezh from scratch if you come from 0.9.0.

------------------------------------------------
Upgrade from old 1.0.0-beta branch to 1.0.0-beta
------------------------------------------------

.. note:: You can use this section if you upgrade from the old 1.0.0-beta branch (it means before 12/01/2015)

^^^^^^^^
With git
^^^^^^^^
Get the last version from GitHub:

.. code-block:: sh

    cd /var/www/sonerezh
    git fetch
    git checkout tags/1.0.0-beta

The dabatase schema has changed, you have to update it (php-cli required):

.. code-block:: sh

    # Follow the instructions given by the command
    app/Console/cake schema update sonerezh

You instance has been upgraded! You can check verify it under the statistics, on the settings page. Do not forget to empty you browser cache and delete the Sonerezh cookies.

^^^^^^^^^^^
Without git
^^^^^^^^^^^
You cannot upgrade Sonerezh if you do not use git. You have to install the new version from scratch.
