===========
Mise à jour
===========

Sonerezh ne propose pas encore de mise à jour automatique. Il faut donc le faire à la main.

------------------------
Mise à jour depuis 0.9.0
------------------------

.. warning:: Malheureusement il n'est pas possible de mettre à jour Sonerezh depuis la version 0.9.0 vers un version supérieure. Ceci est dû aux nombreux changements importants réalisés entre la version 0.9.0 et la version 1.0.0-beta. Il faut repartir de zéro afin d'avoir une installation propre.

----------------------------------------------------------------
Mise à jour depuis l'ancienne branche 1.0.0-beta vers 1.0.0-beta
----------------------------------------------------------------

.. note:: Cette section est valable si vous mettez à jour depuis l'ancienne branche 1.0.0-beta (c'est-à-dire avant le 01/12/2015)

^^^^^^^^
Avec git
^^^^^^^^
Récupérez la dernière version des sources :

.. code-block:: sh

    cd /var/www/sonerezh
    git fetch
    git checkout tags/1.0.0-beta

Le schéma de la base de données à changé, il faut donc le mettre à jour (requiert php-cli) :

.. code-block:: sh
    
    # Suivez les instructions fournies par la commande
    app/Console/cake schema update sonerezh

Votre instance est à jour ! Vous pouvez aller le vérifier sur la page des paramètres, sous les statistiques. Pensez aussi à vider le cache de votre navigateur, et supprimer les cookies de Sonerezh.

^^^^^^^^
Sans git
^^^^^^^^
Malheureusement il n'y a pas de processus de mise à jour si vous n'utilisez pas Git. Vous devez repartir sur une installation vierge.
