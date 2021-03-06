========
Appendix
========

---------------
Troubleshooting
---------------

* I have "404 not found" when I try to access ``www.domain.com/sonerezh/install``

Sonerezh needs the Apache rewrite modules to rewrite its urls. Please check if it is correctly loaded with ``apache2ctl -M``. If you use Nginx, be sure the ``root`` directive is set to the ``webroot`` directory.

* No sound when I try to play a track

If you are running Linux, be sure your browser have the proper codecs to read your files. Furthermore, Sonerezh needs cookies to work, so it is not compatible with the "privacy navigation" mode, unless you add an exception for the domain name where your Sonerezh is hosted.


------------
Known issues
------------

* Sonerezh is not fully compatible with the *Private browsing* mode of your browser (seel also: `#152 <https://github.com/Sonerezh/sonerezh/issues/152>`_).

--------------------------
Nginx server-block example
--------------------------

This is a minimalist configuration sample for Nginx. Feel free to improve it to fit your needs.

.. note:: The example below has been tested with Nginx 1.9.10, under Debian 8.6.

.. code-block:: nginx

    server {
        listen      80;
        server_name demo.sonerezh.bzh;
        root        /var/www/sonerezh/app/webroot;

        index index.php;

        location / {
            try_files $uri $uri/ /index.php?$args;
            expires 14d;
            add_header Cache-Control 'public';
        }

        # The section below handle the thumbnails cache, on the client (browser)
        # side (optional but recommended)
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

            # If fastcgi.conf is not available on your platform you may want to
            # uncomment the following line
            #fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }

If you want to run Sonerezh on a subfolder, like ``www.domain.com/sonerezh``, you can use the server-block below:

.. code-block:: nginx

    server {
        listen      80;
        server_name www.domain.com/sonerezh;

        index index.php;

        location /sonerezh/ {
            alias /var/www/sonerezh/app/webroot/;
            try_files $uri $uri/ /sonerezh//sonerezh/index.php?$args;

            # The section below handle the thumbnails cache, on the client (browser)
            # side (optional but recommended)
            location ~* /([^/]+_[0-9]+x[0-9]+(@[0-9]+x)?\.[a-z]+)$ {
                try_files /img/resized/$1 /index.php?$args;
                add_header Cache-Control 'public';
                expires 14d;
                access_log off;
            }

            location ~ ^/sonerezh/(.+\.php)$ {
                alias /var/www/sonerezh/app/webroot/$1;
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                include fastcgi.conf;

                # If fastcgi.conf is not available on your platform you may want to
                # uncomment the following line
                #fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            }
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
