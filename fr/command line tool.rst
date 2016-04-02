==========================
Outil en ligne de commande
==========================

Depuis la version 1.1.0, Sonerezh propose un outil en ligne de commande vous permettant de traiter les collections contenant un grand nombre de pistes. Cet outil est basé sur le `Shell CakePHP <http://book.cakephp.org/2.0/fr/console-and-shells.html>`_, et peut s'utiliser comme suit.

.. code-block:: sh

    $ cd /var/www/sonerezh/app
    /var/www/sonerezh/app $ Console/cake sonerezh import [OPTIONS] <path>

---------------------------------
Importer des chansons avec la CLI
---------------------------------

Avec la CLI, vous allez pouvoir importer un fichier audio de manière individuelle :

.. code-block:: sh

    /var/www/sonerezh/app $ Console/cake sonerezh import /home/guillaume/Music/file.mp3
    Welcome to CakePHP v2.8.1 Console
    ---------------------------------------------------------------
    App : app
    Path: /var/www/sonerezh/app/
    ---------------------------------------------------------------
    [INFO] You asked to import /home/guillaume/Music/file.mp3. Continue? (yes/no)
    [yes] >
    [INFO] Run import: [100%] [#############################################]

Si le chemin spécifié est un dossier, Sonerezh va scanner son contenu :

.. code-block:: sh

    /var/www/sonerezh/app $ Console/cake sonerezh import /home/guillaume/Music/album-folder
    Welcome to CakePHP v2.8.1 Console
    ---------------------------------------------------------------
    App : app
    Path: /var/www/sonerezh/app/
    ---------------------------------------------------------------
    [INFO] Scan /home/guillaume/Music/album-folder...
    [INFO] Found 13 audio files (0 already in the database). Continue? (yes/no)
    [yes] >
    [INFO] Run import: [100%] [#############################################]

Enfin, vous pouvez aussi demander à Sonerezh de scanner une arborescence de dossiers, avec l'option ``-r`` ou ``--recursive`` :

.. code-block:: sh

    /var/www/sonerezh/app $ Console/cake sonerezh import -r /home/guillaume/Music
    Welcome to CakePHP v2.8.1 Console
    ---------------------------------------------------------------
    App : app
    Path: /var/www/sonerezh/app/
    ---------------------------------------------------------------
    [INFO] Scan /home/guillaume/Music...
    [INFO] Found 614 audio files (13 already in the database). Continue? (yes/no)
    [yes] >
    [INFO] Run import: [100%] [#############################################]

Votre collection devrait maintenant être disponible sur l'interface web de Sonerezh :)
