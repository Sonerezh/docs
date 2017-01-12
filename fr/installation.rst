============
Installation
============

Sonerezh ne requiert pas de manipulation particulière et s'installe comme toute application PHP classique.

------------------------
Installation avec Docker
------------------------

Sonerezh est prévue pour fonctionner sur Docker. C'est d'ailleurs la méthode d'installation la plus sûre et la plus rapide.

^^^^^^^^^^^^^^^
Base de données
^^^^^^^^^^^^^^^

L'image Docker officielle de Sonerezh n'embarque pas de base de données, c'est pourquoi il vous faut un container MariaDB :

.. code-block:: sh

    $ docker run --name sonerezh-db --env MYSQL_ROOT_PASSWORD=motdepasse \
                                    --env MYSQL_USER=sonerezh \
                                    --env MYSQL_PASSWORD=motdepasse \
                                    --env MYSQL_DATABASE=sonerezh \
                                    --volume /path/to/mysql/data:/var/lib/mysql \
                                    --detach mariadb

Où ``/path/to/mysql/data`` est le volume de stockage utilisé par MariaDB (optionnel).

^^^^^^^^^^^^^
L'application
^^^^^^^^^^^^^

Il ne reste plus qu'à déployer l'image de Sonerezh :

.. code-block:: sh

    $ docker run --name sonerezh-app --link sonerezh-db:sonerezh-db \
                                     --volume /path/to/music:/music \
                                     --volume /path/to/thumbnails:/thumbnails \
                                     --detach --publish 8080:80 \
                                     sonerezh/sonerezh:latest

Où ``/path/to/music`` est le chemin sur votre hôte où est stockée votre musique. Et où ``/path/to/thumbnails`` est le chemin sur votre hôte où Sonerezh peut sauvegarder les miniatures de vos albums.

L'option ``--publish 8080:80`` rend Sonerezh accessible sur le port 8080 de l'hôte (http://127.0.0.1:8080).

-------------------------------------
Installation sur un hébergement dédié
-------------------------------------

Nous vous recommandons d'utiliser ``git`` pour récupérer les sources du projet, cela facilitera le processus de mise à jour.

.. note:: Nous allons installer sonerezh dans ``/var/www/sonerezh``, pour pouvoir y accéder à l'adresse http://demo.sonerezh.bzh.

On commence par préparer la base de données :

.. code-block:: sh

    mysql -u root -p

.. code-block:: sql

    CREATE DATABASE sonerezh;
    GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY 'votre-motdepasse';
    FLUSH PRIVILEGES;
    exit;

.. note:: Cette étape peut aussi être réalisée via PHPMyAdmin si vous l'utilisez déjà.

Installation avec Git :

.. code-block:: sh

    cd /var/www
    sudo git clone --branch master https://github.com/Sonerezh/sonerezh.git
    sudo chown -R www-data: sonerezh/

    Si vous préférez télécharger une archive Zip depuis GitHub:

.. code-block:: sh

    cd /var/www
    sudo wget https://github.com/Sonerezh/sonerezh/archive/1.1.3.zip
    sudo unzip 1.1.3.zip
    sudo mv sonerezh-1.1.3 sonerezh
    sudo chown -R www-data: sonerezh

^^^^^^^^^^^^^^^^^^^^^^^^^^
Préparation du serveur web
^^^^^^^^^^^^^^^^^^^^^^^^^^

Des modèles de configuration pour Nginx et Apache sont disponibles en :doc:`appendix`.

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
* Hôte : le nom d'hôte de la base de données pour Sonerezh (ajoutez :1234 si vous utilisez un port non standard)
* Base de données : le nom de la base de données
* Identifiant : l'identifiant de l'utilisateur MySQL ou MariaDB
* Mot de passe : le mot de passe de l'utilisateur MySQL ou MariaDB
* Préfixe (optionnel) : si vous souhaitez ajouter un préfixe au nom des tables (exemple : snrzh\_)

5) Validez. C'est bon ! :)

.. _sur notre dépôt GitHub: https://github.com/Sonerezh/sonerezh/archive/1.1.3.zip

----------------------------------------
Exemple de déploiement sur Ubuntu Server
----------------------------------------
Voici un exemple d'installation réalisée sur Ubuntu Server 14.10 (Apache 2.4, PHP 5.5 et MySQL 14.14). Dans cet exemple, le dossier dans lequel nous déployons Sonerezh est ``/var/www/html/sonerezh`` et l'URL d'accès : http://www.monserveur.com/sonerezh.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Télécharger les sources du projet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Comme indiqué ci-dessus, nous utilisons Git pour récupérer les sources du projet, cela facilitera le processus de mise à jour dans le futur (si la commande Git n'est pas disponible : ``sudo apt-get install git``).

.. code-block:: sh

    cd /var/www/html
    sudo git clone --branch master https://github.com/Sonerezh/sonerezh.git
    sudo chown -R www-data: sonerezh/

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Préparation de la base de données
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1) Se connecter à la console MySQL :

.. code-block:: sh

    mysql -u root -p

2) Créer la base de données, y associer un utilisateur et lui affecter des droits :

.. code-block:: sql

    CREATE DATABASE sonerezh;
    GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY 'votre-motdepasse';
    FLUSH PRIVILEGES;
    exit;

.. note:: Cette étape peut aussi être réalisée via PHPMyAdmin si vous l'utilisez déjà.

^^^^^^^^^^^^^^^^^^^^^^^^^
Configurer le serveur web
^^^^^^^^^^^^^^^^^^^^^^^^^
S'assurer que le module Apache ``mod_rewrite`` est activé :

.. code-block:: sh

    sudo a2enmod rewrite

Préparer le fichier de configuration :

.. code-block:: sh

    sudo vim /etc/apache2/sites-available/sonerezh.conf

Et y ajouter le Virtual Host suivant :

.. code-block:: apache

   <VirtualHost *:80>
        ServerName      www.monserveur.com
        DocumentRoot    /var/www/html/sonerezh

        <Directory /var/www/html/sonerezh>
            Options -Indexes
            AllowOverride All
            <IfModule mod_authz_core.c>
                Require all granted
            </IfModule>
        </Directory>

        CustomLog   /var/log/apache2/www.monserveur.com-access.log "Combined"
        ErrorLog    /var/log/apache2/www.monserveur.com-error.log
    </VirtualHost>

Enregistrer le fichier, activer le nouveau site et redémarrer Apache :

.. code-block:: sh

    sudo a2ensite sonerezh && sudo service apache2 restart

^^^^^^^^^^^^^^^^^^
Installer Sonerezh
^^^^^^^^^^^^^^^^^^
Nous y sommes presque, il ne reste plus qu'à accéder à http://www.monserveur.com/sonerezh et de remplir les champs avec les informations ci-dessus. Et c'est parti !
