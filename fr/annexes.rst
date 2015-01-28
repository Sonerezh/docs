=======
Annexes
=======

---------------------------------
Modèle de server-block pour Nginx
---------------------------------

Voici un modèle fonctionnel de server-block a ajouter dans votre configuration Nginx. Celui-ci n'est évidemment pas exhaustif et ne propose que le minimum de fonctionnalités (pas de HTTPS par exemple).

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

        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_index index.php;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            include /etc/nginx/fastcgi_params;
        }
    }

De nombreux tutoriels sur Internet vous aideront à configurer Nginx avec PHP si ce n'est pas déjà fait.

----------------------------------
Modèle de virtualhost pour Apache2
----------------------------------

Voici un modèle fonctione de virtual host a ajouter dans votre configuration Apache. Celui-ci n'est évidemment pas exhaustif et ne propose que le minimum de fonctionnalités (pas de HTTPS par exemple).

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
