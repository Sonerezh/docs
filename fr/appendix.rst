=======
Annexes
=======

----------------
FAQ / Diagnostic
----------------

* J'obtiens "404 not found" lorsque j'essaye d'accéder à ``www.domain.com/sonerezh/install``

Sonerezh utilise le module rewrite d'Apache pour réécrire ses urls. Vérifiez qu'il est bien activé avec la commande ``apache2ctl -M``. Si vous utilisez Nginx, vérifiez que la directive ``root`` de votre server-block pointe bien sur le dossier ``webroot`` de Sonerezh.

* Pas de son lorsque je lance une piste

Si vous êtes sous Linux, assurez-vous que votre navigateur dispose des codecs adaptés au format audio des fichiers que vous souhaitez lire. De plus, Sonerezh a besoin de ses propres cookies pour fonctionner, et n'est donc pas compatible avec le mode navigation privée, à moins d'ajouter une exception sur le domaine hébergeant votre instance de Sonerezh.

----------------
Problèmes connus
----------------

* Sonerezh n'est pas compatible avec le mode *Navigation privée* de votre navigateur (voir aussi: `#152 <https://github.com/Sonerezh/sonerezh/issues/152>`_).

---------------------------------
Modèle de server-block pour Nginx
---------------------------------

Voici un modèle fonctionnel de server-block à ajouter dans votre configuration Nginx. Celui-ci n'est évidemment pas exhaustif et ne propose que le minimum de fonctionnalités (pas de HTTPS par exemple).

.. note:: Le modèle ci-dessous a été testé avec Nginx 1.9.10, sous Debian 8.6. Il permet d'avoir une instance de Sonerezh accessible à l'adresse http://demo.sonerezh.bzh.

.. code-block:: nginx

    server {
        listen      80;
        server_name demo.sonerezh.bzh;
        root        /var/www/sonerezh/app/webroot;

        index index.php;

        location / {
            try_files $uri $uri/ /index.php?$args;
        }

        # Le bloc suivant permet de gérer la mise en cache des miniatures
        # et des pochettes d'album côté client (optionnel mais recommandé)
        location ~* /([^/]+_[0-9]+x[0-9]+(@[0-9]+x)?\.[a-z]+)$ {
            try_files /img/resized/$1 /index.php?$args;
            add_header Cache-Control 'public';
            expires 14d;
            access_log off;
        }

        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_index index.php;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            include fastcgi.conf;

            # Si fastcgi.conf n'est pas disponible sur votre plateforme vous
            # pouvez décommenter la ligne suivante
            #fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }

Si vous souhaiter faire fonctionner Sonerezh sur un sous-dossier, comme par exemple ``www.domain.com/sonerezh``, vous pouvez vous inspirer de l'exemple ci-dessus :

.. code-block:: nginx

    server {
        listen      80;
        server_name www.domain.com/sonerezh;

        index index.php;

        location /sonerezh/ {
            alias /var/www/sonerezh/app/webroot/;
            try_files $uri $uri/ /sonerezh//sonerezh/index.php?$args;

            # Le bloc suivant permet de gérer la mise en cache des miniatures
            # et des pochettes d'album côté client (optionnel mais recommandé)
            location ~* /([^/]+_[0-9]+x[0-9]+(@[0-9]+x)?\.[a-z]+)$ {
                alias /var/www/sonerezh/app/webroot/;
                try_files /img/resized/$1 /sonerezh/index.php?$args;
                add_header Cache-Control 'public';
                expires 14d;
                access_log off;
            }

            location ~ ^/sonerezh/(.+\.php)$ {
                alias /var/www/sonerezh/app/webroot/$1;
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                include fastcgi.conf;

                # Si fastcgi.conf n'est pas disponible sur votre plateforme vous
                # pouvez décommenter la ligne suivante
                #fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            }
        }
    }

De nombreux tutoriels sur Internet vous aideront à configurer Nginx avec PHP si ce n'est pas déjà fait.

----------------------------------
Modèle de virtualhost pour Apache2
----------------------------------

Voici un modèle fonctione de virtual host à ajouter dans votre configuration Apache. Celui-ci n'est évidemment pas exhaustif et ne propose que le minimum de fonctionnalités (pas de HTTPS par exemple).

.. note:: Le modèle si-dessous a été testé avec Apache 2.2.22, sous Debian 7.8. Il permet d'avoir une instance de Sonerezh accessible à l'adresse http://demo.sonerezh.bzh.

.. code-block:: apache

    <VirtualHost *:80>
        ServerName      demo.sonerezh.bzh
        DocumentRoot    /var/www/sonerezh

        <Directory /var/www/sonerezh>
            Options -Indexes
            AllowOverride All

            # Apache 2.2.x
            <IfModule !mod_authz_core.c>
                Order Allow,Deny
                Allow from all
            </IfModule>

            # Apache 2.4.x
            <IfModule mod_authz_core.c>
                Require all granted
            </IfModule>
        </Directory>

        CustomLog   /var/log/apache2/demo.sonerezh.bzh-access.log "Combined"
        ErrorLog    /var/log/apache2/demo.sonerezh.bzh-error.log
    </VirtualHost>
