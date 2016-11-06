
Docker Concepts
########

Image
*****
This is the starting point. You can either start from an existing image on `Docker Hub <https://hub.docker.com/>`_ or create your own image by adding layers to the root or original one found on `Docker Hub <https://hub.docker.com/>`_.

* List images: ``docker images``
* List images and their intermediate layers: ``docker images -a``


Container
*********
A Docker container is created from an existing image.

* ``docker run -p 8000:80 -d nginx``


Useful commands
###############
* List all active containers: ``docker ps``
* Delete all active containers: ``docker rm $(docker ps -a -q)``

