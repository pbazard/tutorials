

Cache management
================

Configuring Cache-Control and Expire headers
--------------------------------------------
Addition to the ETag file validation header. Cache-Control response header is newer and offers a more fine-grained control than the Expire header.

With ``Nginx``, we can use the header module, which is a core Nginx module, to configure these headers. This module is added to the default
server block configuration file.

  ``sudo vi /etc/nginx/nginx.conf``
  
Find the ``server`` configuration block and add a ``map`` block before:

  # Expires map
  map $sent_http_content_type $expires {
    default                off;
    text/html              epoch;
    text/css               max;
    application/javascript max;
    ~image/                max;
  }
