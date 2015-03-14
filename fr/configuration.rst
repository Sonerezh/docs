=============
Configuration
=============
La configuration de Sonerezh s'effecture globalement sur la page /settings de votre instance. Cette page vous permet aussi d'obtenir un certain nombre de statistiques sur la taille de votre librairie, ou encore l'espace occupé par les différents caches.

Cette page détaille l'ensemble des paramètres disponibles.

---------------------------
Emplacement de la librairie
---------------------------
Indiquez ici le chemin absolu du dossier dans lequel Sonerezh doit aller chercher votre musique.

.. tip:: Assurez-vous que Sonerezh a les droits de lecture, de façon récursive, sur ce dossier.
.. warning:: Nous vous déconseillons de stocker votre musique dans le dossier de l'application (app/ et ses sous-répertoires).

-------------------------------
Activer les notifications email
-------------------------------
Active ou non les notifications par email. Par exemple Sonerezh peut envoyer un message de bienvenue aux nouveaux utilisateurs. Si vous activez cette option, assurez-vous que PHP puisse envoyer des emails.

Tout comme les bases de données, la configuration d'email peut être centralisée dans une classe intitulé ``EmailConfig``, présente dans le fichier ``app/Config/email.php``. Le fichier ``app/Config/email.php.default`` fournit un exemple, vous pouvez donc le copier / coller.

Vous pouvez vous référer à `la documentation officielle CakePHP <http://book.cakephp.org/2.0/fr/core-utility-libraries/email.html>`_ pour configurer les différentes méthodes de transport, néanmoins la configuration suivante devrait suffire sur la plupart des installations (sous réserve d'un MTA disponible) :

.. code-block:: php

    <?php
    class EmailConfig {
        public $default = array(
            'transport' => 'Mail',
            'from' => 'no-reply@sonerezh.bzh',
            'charset' => 'utf-8',
            'headerCharset' => 'utf-8',
        );
    } 

Ainsi, Sonerezh enverra les emails en utilisant la commande PHP ``mail()``.

---------------------------------
Conversion automatique des pistes
---------------------------------
Si votre collection contient des pistes dans des formats qui ne sont pas encore supportés par nos navigateurs, Sonerezh peut convertir celles-ci en MP3 ou OGG/Vorbis avant de les diffuser.

.. tip:: Sonerezh utilise ``avconv`` pour réaliser les conversions, cette fonctionnalité est donc dépendante de la présence de ``libav-tools`` sur votre machine.

-----------------------------
Gestion de la base de données
-----------------------------
La page de paramètres vous permet de réaliser quelques opérations de base sur la base de données de Sonerezh, ainsi que sur son cache :

* Mise à jour de la base de données : lance le processus d'import de votre collection. Utile si vous avez ajouté de nouvelles pistes récemment;
* Nettoyer le cache : vide le cache de Sonerezh (pistes converties, pochettes redimensionnées);
* Réinitialiser la base de données : réinitialise la base de données Sonerezh. Toutes les pistes et playlists **SERONT PERDUES**. Notez que Sonerezh ne vide que les tables ``songs`` et ``playlist_memberships`` et ne touche en aucun cas à vos fichiers;

------------
Statistiques
------------
Vous pouvez aussi obtenir quelques statistiques à propos de Sonerezh :

* Nombre d'artistes (correspond aux **artistes d'albums** (balise ``band``))
* Nombre d'albums
* Nombre de pistes
* Taille du cache des images (correspond aux pochettes d'album redimensionnées, placées dans ``app/webroot/img/resized/``
* Taille du cache des pistes (correspond aux pistes converties, placées dans ``app/tmp/*.{ogg,mp3}``
