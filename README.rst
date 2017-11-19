dockit
------

A Bash script for easy building and running of Docker images
using the Dockerfile in the current woring directory for building
and the name of the current working directory as the image name.

Suppose you have following directory structure (`$DOCKIT` below refers to
the `dockit` directory shown here):

.. code-block::

  dockit
  |── python363
  │   └── Dockerfile
  └── node891
      └── Dockerfile

The python363/Dockerfile contains:

.. code-block:: Dockerfile

    FROM python:3.6.3-alpine

The node891/Dockerfile contains:

.. code-block:: Dockerfile

    FROM node:8.9.1-alpine


Then you can build or update a Docker image for each of those by running:

.. code-block:: shell

    cd $DOCKIT/python363
    dockit build

.. code-block:: shell

    cd $DOCKIT/node891
    dockit build

The image names will be `python363` and `node891`, respectively.

Once the images have been built, you can run them like so:

.. code-block:: shell

    cd $DOCKIT/python363
    dockit run

Add ``--rm`` if you want to remove the container upon exit.

You can of course install extra utilities into the images, give
them a default command, and otherwise configure the image using
the Dockerfile. For example, my `python363` image installs
the latest versions of pip and ipython, and sets the default
command to ipython with the following Dockerfile:

.. code-block:: Dockerfile

    FROM python:3.6.3-alpine

    CMD ipython

    RUN pip install -U pip
    RUN pip install ipython


Running ``dockit run --rm`` then drops me into a throwaway ipython shell
in the container that will be deleted when I exit ipython.

.. warning::

    If you use Docker to experiment with miscellaneous code or resources
    from untrusted parties, make sure you have Docker's userns-remap_ feature
    configured or run the container as a non-root user (e.g., --user nobody).

.. _userns-remap: https://docs.docker.com/engine/security/userns-remap/
