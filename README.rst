dockit
------

A Bash script for easy building and running of Docker images
using the Dockerfile in the current woring directory for building
and the name of the current working directory as the image name.

The idea is that if you have a directory like ``$HOME/dockertmp`` that
contains directories for different experimental images, each of which
contains a Dockerfile, using the name of the directory containing
the Dockerfile as the name of the image when building and running,
and always supplying the common '-it' args when running,
is convenient.

Example:

.. code-block:: shell-session

    $ mkdir -p $HOME/dockertmp
    $ cd $HOME/dockertmp
    $ mkdir python352
    $ cd python352
    $ cat <<EOF > Dockerfile
    FROM python:3.5.2-alpine
    EOF
    $ dockit build
    Sending build context to Docker daemon 2.048 kB
    Step 1 : FROM python:3.5.2-alpine
     ---> 9a646c8ffe06
    Successfully built 9a646c8ffe06
    $ dockit run --rm
    Python 3.5.2 (default, Jul  8 2016, 19:25:07)
    [GCC 5.3.0] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> print("Hello, world")
    Hello, world
    >>>
    $ cd ..
    $ mkdir node69
    $ cd node69
    $ cat <<EOF > Dockerfile
    FROM node:6.9-alpine
    EOF
    $ dockit build
    Sending build context to Docker daemon 2.048 kB
    Step 1 : FROM node:6.9-alpine
     ---> 4c013cd428c0
    Successfully built 4c013cd428c0
    $ dockit run --rm
    > console.log("Hello, world")
    Hello, world
    $
