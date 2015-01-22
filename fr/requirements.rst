Pré-requis
==========

Serveur web
-----------
Sonerezh est une application web accessible avec votre navigateur. Elle a donc besoin d'un serveur web pour fonctionner (Apache, Nginx, etc). Bien que nous fournissons des modèles de configuration pour Apache et Nginx, nous ne détaillerons pas comment installer un serveur web.

Base de données
---------------
Sonerezh s'appuie sur une base de données MySQL ou MariaDB pour fonctionner. La base de données doit être créée avant de lancer l'installation.

1) Connectez-vous à votre gestionnaire de base de données :

.. code-block:: sh

    mysql -u root -p

2) Créez la base de données pour Sonerezh, et créez un utilisateur pour l'application :

.. code-block:: sql

    CREATE DATABASE sonerezh;
    GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY 'password';
    FLUSH PRIVILEGES;
    exit;

PHP
---
Sonerezh fonctionne avec le framework PHP CakePHP, PHP est donc indispensable.

* PHP 5.4 ou supérieur
* Le module PHP GD

Libav (optionnel)
-----------------
Si vous souhaitez que Sonerezh puisse réencoder vos pistes qui en ont besoin vers un format lisible par votre navigateur, vous devez installer libav-tools.

Installation sur Debian et dérivées :

.. code-block:: sh

    sudo apt-get install libav-tools
