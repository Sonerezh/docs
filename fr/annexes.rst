=======
Annexes
=======

---------------------------------
Modèle de server-block pour Nginx
---------------------------------

Voici un modèle fonctionnel de server-block à ajouter dans votre configuration Nginx. Celui-ci n'est évidemment pas exhaustif et ne propose que le minimum de fonctionnalités (pas de HTTPS par exemple).

.. note:: Le modèle ci-dessous a été testé avec Nginx 1.6.2, sous Debian 7.8. Il permet d'avoir une instance de Sonerezh accessible à l'adresse http://demo.sonerezh.bzh.

.. code-block:: nginx

    server {
        listen      80;
        server_name demo.sonerezh.bzh;
        root        /var/www/sonerezh/app/webroot;

        index index.php;

        location / {
            try_files $uri $uri/ /index.php?$args;
        }

        # Serve static images from resized folder
        location ~* \/([^\/]+_[0-9]+x[0-9]+\.[a-z]+) {
            try_files /img/resized/$1 /index.php?$args;
            expires 14d;
            add_header Cache-Control 'public';
        }

        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_index index.php;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include /etc/nginx/fastcgi_params;
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

            # Serve static images from resized folder
            location ~* \/([^\/]+_[0-9]+x[0-9]+\.[a-z]+) {
                alias /var/www/sonerezh/app/webroot/;
                try_files /img/resized/$1 /sonerezh/index.php?$args;
                expires 21d;
                access_log off;
                add_header Cache-Control 'public';
            }

            location ~ ^/sonerezh/(.+\.php)$ {
                alias /var/www/sonerezh/app/webroot/$1;
                #try_files $uri =404
                fastcgi_pass php5-fpm-sonerezh-sock;
                fastcgi_index index.php;
                include fastcgi.conf;
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
