
Nginx Configuration File's Structure
====================================
Nginx consists of modules which are controlled by directives. Directives comes in two flavours: simple directives and block directives.

  .. code-block:: ini
  
      http {
        server {
          location / {
            root /data/www;
          }
          
          location /images/ {
            root /data;
          }
        }
      }


Serving Static Content
======================



Cache Management
================

Configuring Cache-Control and Expire headers
--------------------------------------------
Addition to the ETag file validation header. Cache-Control response header is newer and offers a more fine-grained control than the Expire header.

With ``Nginx``, we can use the `header module <http://nginx.org/en/docs/http/ngx_http_headers_module.html>`_, which is a core Nginx module, to configure these headers. This module is added to the default
server block configuration file.

  ``sudo vi /etc/nginx/nginx.conf``
  
A ``map`` block defines the mapping between a file type and how long it will be cached. Find the ``server`` configuration block and add a ``map`` block before:

  .. code-block:: ini
  
    # Expires map
    map $sent_http_content_type $expires {
      default                off;
      text/html              epoch; # no caching ask for the page on every request
      text/css               max;   # cache the files as long as possible
      application/javascript max;
      ~image/                max;   # regexp to map all the file types containing image/ in their MIME type 
    }
    
    server {
      listen 80 default_server;
      listen [::]:80 default_server;
    
      expires $expires;
      ...
    }

Testing Browser Caching
-----------------------
Execute the following request:

  curl -I http://localhost/test.html
  
and check that ``Expires`` and ``Cache-Control`` are present.
