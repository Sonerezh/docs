============
Installation
============

Sonerezh ne requiert pas de manipulations particulières et s'installe comme toute application PHP classique.

-------------------------------------
Installation sur un hébergement dédié
-------------------------------------

Nous vous recommandons d'utiliser ``git`` pour récupérer les sources du projet, cela facilitera le processus de mise à jour.

.. note:: Nous allons installer sonerezh dans ``/var/www/sonerezh``, pour pouvoir y accéder à l'adresse http://demo.sonerezh.bzh.

Vous pouvez utiliser Git ou bien récupérer une archive au format ZIP sur le dépôt GitHub de Sonerezh.

Installation avec Git :

.. code-block:: sh

    cd /var/www
    sudo git clone https://github.com/Sonerezh/sonerezh.git
    sudo chown -R wwww-data: sonerezh/ && sudo chmod -R 775 sonerezh/

Installation sans Git :

.. code-block:: sh

    cd /var/www
    sudo wget https://github.com/Sonerezh/sonerezh/archive/master.zip
    sudo unzip master.zip
    sudo chown -R www-data: sonerezh-master/ && sudo chmod -R 775 sonerezh-master/

^^^^^^^^^^^^^^^^^^^^^^^^^^
Préparation du serveur web
^^^^^^^^^^^^^^^^^^^^^^^^^^

Des modèles de configuration pour Nginx et Apache sont disponibles en :doc:`annexes`.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Déploiement de l'application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

C'est prêt ! Vous n'avez plus qu'à vous rendre sur http://demo.sonerezh.bzh/install et à remplir les informations demandées (à adapter à votre configuration).

* Email : l'adresse email utilisée pour vous connecter, ce premier compte sera créé avec le niveau d'accès administrateur
* Mot de passe : mot de passe de l'administrateur
* Dossier musique : le dossier dans lequel se trouve votre musique
* Hôte : le nom d'hôte de la base de données pour Sonerezh
* Base de données : le nom de la base de données
* Identifiant : l'identifiant de l'utilisateur MySQL ou MariaDB
* Mot de passe : le mot de passe de l'utilisateur MySQL ou MariaDB
* Préfixe (optionnel) : si vous souhaitez ajouter un préfixe au nom des tables (exemple : snrzh\_)

Validez, et c'est bon ! :)

-----------------------------------------
Installation sur un hébergement mutualisé
-----------------------------------------

Les hébergements de type mutualisés ne vous permettent pas un accès complet. La configuration du nom de domaine ou de votre espace dépendant de votre hébergeur, nous ne détaillerons pas ces étapes.

.. note:: Nous allons déployer les sources dans ``sonerezh/``, à l'adresse http://demo.sonerezh.bzh.

1) Récupérez votre copie de sonerezh `sur notre dépôt GitHub`_
2) Déposez cette archive sur votre hébergement et décompressez-la dans ``sonerezh/``
3) Rendez-vous sur http://demo.sonerezh.bzh/install
4) Remplissez les champs 

* Email : l'adresse email utilisée pour vous connecter, ce premier compte sera créé avec le niveau d'accès administrateur
* Mot de passe : mot de passe de l'administrateur
* Dossier musique : le dossier dans lequel se trouve votre musique
* Hôte : le nom d'hôte de la base de données pour Sonerezh
* Base de données : le nom de la base de données
* Identifiant : l'identifiant de l'utilisateur MySQL ou MariaDB
* Mot de passe : le mot de passe de l'utilisateur MySQL ou MariaDB
* Préfixe (optionnel) : si vous souhaitez ajouter un préfixe au nom des tables (exemple : snrzh\_)

5) Validez. C'est bon ! :)

.. _sur notre dépôt GitHub: https://github.com/Sonerezh/sonerezh/archive/master.zip
