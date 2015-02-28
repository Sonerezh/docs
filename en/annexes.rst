=======
Annexes
=======

--------------------------
Nginx server-block example
--------------------------

This is a minimalist configuration sample for Nginx. Feel free to improve it to fit your needs.

.. note:: This example has been tested with Nginx 1.6.2, under Debian 7.8.

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

Many tutorials on the web can help you to configure Nginx and PHP-FPM.

----------------------------
Apache2 virtual host example
----------------------------

This is a minimalist configuration sample for Apache 2. Feel free to improve it to fit your needs.

.. note:: This example has been tested with Apache 2.2.22, under Debian 7.8.

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
