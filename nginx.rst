Nginx
=====

Which version: 

  sudo nginx -v

Check if your syntax is error free:

  sudo nginx -t

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

How Ngix processes a request
============================
First, Nginx decides which ``server`` should process the request. The test is based on the content of the header field ``Host``. If the value does not match any server name, the request will be routed to the default server; the first one in our case but it can be set explicitly by defining the ``default_server`` parameter in the ``listen`` directive.

Serving Static Content
======================



Setting Up a Simple Proxy Server
================================
First define the proxied server by adding one more server block:

 .. code-block:: ini
  
      server {
        listen 8080;
        root /data/up1;
        
        location / {
        }
      }

Next, we use the...

 .. code-block:: ini
  
  location ~ \.(gif|jpg|png)$ {
    root /data/images;
  }

The parameter ``~ \.(gif|jpg|png)$`` is a regular expression matching all URI ending with ``.gif``, ``.jpg``, ``.png``. A **regular expression** should be preceded by ``~``.

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

HTTP/2 support
==============
Reference `Digital Ocean <https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-with-http-2-support-on-ubuntu-16-04>`_. The main advantage of HTTP/2 is its high transfer speed for **content-rich** websites.

Modify the listening port to 443, which is used by the HTTPS protocol:

  .. code-block:: ini
    
    listen 443 ssl http2 default_server;
    listen [::]:443 ssl http2 default_server;
    
Redirecting all HTTP requests to HTTPS
--------------------------------------
At the bottom of your file, create a new ``server`` block for redirecting all HTTP requests to HTTPS:

    .. code-block:: ini
    
      server {
       listen         80;
       listen    [::]:80;
       server_name    example.com;
       return         301 https://$server_name$request_uri;
      }

Veryfing the changes
--------------------
Check that everything works properly in Chrome.
