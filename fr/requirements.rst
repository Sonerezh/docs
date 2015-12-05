==========
Pré-requis
==========

-----------
Serveur web
-----------

Sonerezh est une application web accessible avec votre navigateur. Elle a donc besoin d'un serveur web pour fonctionner (Apache, Nginx, etc). Bien que nous fournissons des modèles de configuration pour Apache et Nginx, nous ne détaillerons pas comment installer un serveur web.

.. note:: Apache a besoin du module ``mod_rewrite`` pour interpréter les URLs de Sonerezh correctement. Pour l'activer sur Debian et dérivés : ``sudo a2enmod rewite && sudo service apache2 restart``.

---------------
Base de données
---------------

Sonerezh s'appuie sur une base de données pour stocker ses données. Celle-ci peut être gérée par MariaDB, MySQL ou PostgreSQL mais nous recommandons MariaDB/MySQL.
Elle doit être créée avant de lancer l'installation.

1) Connectez-vous au gestionnaire de base de données :

.. code-block:: sh

    mysql -u root -p

2) Créez la base de données pour Sonerezh, et créez un utilisateur pour l'application :

.. code-block:: sql

    CREATE DATABASE sonerezh;
    GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY 'password';
    FLUSH PRIVILEGES;
    exit;

---
PHP
---

Sonerezh fonctionne avec le framework PHP CakePHP, PHP est donc indispensable.

* PHP 5.4 ou supérieur
* Le module PHP GD

Vérifiez que les extensions PHP requises sont bien activées dans votre php.ini:

.. code-block:: ini
    
    extension=exif.so
    extension=gd.so
    extension=pdo_mysql.so

-----------------
Libav (optionnel)
-----------------

Si vous souhaitez que Sonerezh puisse réencoder vos pistes qui en ont besoin vers un format lisible par votre navigateur, vous devez installer libav-tools.

Installation sur Debian et dérivées :

.. code-block:: sh

    sudo apt-get install libav-tools
