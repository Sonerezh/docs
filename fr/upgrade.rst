===========
Mise à jour
===========

Sonerezh ne propose pas encore de mise à jour automatique. Il faut donc le faire à la main.

---------------------
0.9.0 vers 1.0.0-beta
---------------------

.. warning:: Malheureusement il n'est pas possible de mettre à jour Sonerezh depuis la version 0.9.0 vers un version supérieure. Ceci est dû aux nombreux changements importants réalisés entre la version 0.9.0 et la version 1.0.0-beta. Il faut repartir de zéro afin d'avoir une installation propre.

---------------------
1.0.0-beta vers 1.0.0
---------------------

.. note:: Cette section est valable si vous mettez à jour depuis l'ancienne branche 1.0.0-beta

^^^^^^^^
Avec git
^^^^^^^^
Récupérez la dernière version des sources :

.. code-block:: sh

    $ cd /var/www/sonerezh
    /var/www/sonerezh $ git fetch
    /var/www/sonerezh $ git checkout tags/1.0.0

Le schéma de la base de données à changé, il faut donc le mettre à jour (requiert php-cli) :

.. code-block:: sh

    # Suivez les instructions fournies par la commande
    /var/www/sonerezh $ app/Console/cake schema update sonerezh

Votre instance est à jour ! Vous pouvez aller le vérifier sur la page des paramètres, sous les statistiques. Pensez aussi à vider le cache de votre navigateur, et supprimer les cookies de Sonerezh.

^^^^^^^^
Sans git
^^^^^^^^
Malheureusement il n'y a pas de processus de mise à jour si vous n'utilisez pas Git. Vous devez repartir sur une installation vierge.

---------------------
1.0.0 vers 1.1.0-beta
---------------------

^^^^^^^^
Avec git
^^^^^^^^
Récupérez la dernière version des sources :

.. code-block:: sh

    $ cd /var/www/sonerezh
    /var/www/sonerezh $ git fetch
    /var/www/sonerezh $ git checkout tags/1.1.0

Votre instance est à jour ! Vous pouvez aller le vérifier sur la page des paramètres, sous les statistiques. Penses aussi à vider le cache de votre navigateur.

^^^^^^^^
Sans git
^^^^^^^^
Il n'y pas de procédure officielle pour mettre à jour Sonerezh sans Git. Nous vous conseillons de repartir sur une installation neuve. Cependant, l'outil ``rsync`` devrait fonctionner :

.. code-block:: sh

    $ cd /var/www
    /var/www $ cp -a sonerezh sonerezh.backup
    /var/www $ wget https://github.com/Sonerezh/sonerezh/archive/1.1.0-beta.tar.gz
    /var/www $ tar -zcf 1.1.0-beta.tar.gz
    /var/www $ rsync -a sonerezh-1.1.0-beta sonerezh
