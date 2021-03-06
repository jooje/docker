:title: Hello world example
:description: A simple hello world example with Docker
:keywords: docker, example, hello world

.. _examples:

Hello World
-----------

.. _running_examples:

Check your Docker install
-------------------------

This guide assumes you have a working installation of Docker. To check
your Docker install, run the following command:

.. code-block:: bash

    # Check that you have a working install
    docker info

If you get ``docker: command not found`` or something like
``/var/lib/docker/repositories: permission denied`` you may have an incomplete
Docker installation or insufficient privileges to access docker on your machine.

Please refer to :ref:`installation_list` for installation instructions.


.. _hello_world:

Hello World
===========

.. include:: example_header.inc

This is the most basic example available for using Docker.

Download the base image which is named ``ubuntu``:

.. code-block:: bash

    # Download an ubuntu image
    sudo docker pull ubuntu

Alternatively to the ``ubuntu`` image, you can select ``busybox``, a bare
minimal Linux system. The images are retrieved from the Docker
repository.


.. code-block:: bash

    sudo docker run ubuntu /bin/echo hello world

This command will run a simple ``echo`` command, that will echo ``hello world`` back to the console over standard out.

**Explanation:**

- **"sudo"** execute the following commands as user *root* 
- **"docker run"** run a command in a new container 
- **"ubuntu"** is the image we want to run the command inside of.
- **"/bin/echo"** is the command we want to run in the container
- **"hello world"** is the input for the echo command



**Video:**

See the example in action

.. raw:: html

   <iframe width="560" height="400" frameborder="0"
           sandbox="allow-same-origin allow-scripts" 
   srcdoc="<body><script type=&quot;text/javascript&quot; 
           src=&quot;https://asciinema.org/a/2603.js&quot; 
           id=&quot;asciicast-2603&quot; async></script></body>">
   </iframe>

----

.. _hello_world_daemon:

Hello World Daemon
==================

.. include:: example_header.inc

And now for the most boring daemon ever written!

We will use the Ubuntu image to run a simple hello world daemon that will just print hello
world to standard out every second. It will continue to do this until
we stop it.

**Steps:**

.. code-block:: bash

    CONTAINER_ID=$(sudo docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done")

We are going to run a simple hello world daemon in a new container
made from the ``ubuntu`` image.

- **"sudo docker run -d "** run a command in a new container. We pass "-d"
  so it runs as a daemon.
- **"ubuntu"** is the image we want to run the command inside of.
- **"/bin/sh -c"** is the command we want to run in the container
- **"while true; do echo hello world; sleep 1; done"** is the mini
  script we want to run, that will just print hello world once a
  second until we stop it.
- **$CONTAINER_ID** the output of the run command will return a
  container id, we can use in future commands to see what is going on
  with this process.

.. code-block:: bash

    sudo docker logs $CONTAINER_ID

Check the logs make sure it is working correctly.

- **"docker logs**" This will return the logs for a container
- **$CONTAINER_ID** The Id of the container we want the logs for.

.. code-block:: bash

    sudo docker attach -sig-proxy=false $CONTAINER_ID

Attach to the container to see the results in real-time.

- **"docker attach**" This will allow us to attach to a background
  process to see what is going on.
- **"-sig-proxy=false"** Do not forward signals to the container; allows
  us to exit the attachment using Control-C without stopping the container.
- **$CONTAINER_ID** The Id of the container we want to attach too.

Exit from the container attachment by pressing Control-C.

.. code-block:: bash

    sudo docker ps

Check the process list to make sure it is running.

- **"docker ps"** this shows all running process managed by docker

.. code-block:: bash

    sudo docker stop $CONTAINER_ID

Stop the container, since we don't need it anymore.

- **"docker stop"** This stops a container
- **$CONTAINER_ID** The Id of the container we want to stop.

.. code-block:: bash

    sudo docker ps

Make sure it is really stopped.


**Video:**

See the example in action

.. raw:: html

   <iframe width="560" height="400" frameborder="0"
           sandbox="allow-same-origin allow-scripts" 
   srcdoc="<body><script type=&quot;text/javascript&quot; 
           src=&quot;https://asciinema.org/a/2562.js&quot; 
           id=&quot;asciicast-2562&quot; async></script></body>">
   </iframe>

The next example in the series is a :ref:`python_web_app` example, or
you could skip to any of the other examples:


* :ref:`python_web_app`
* :ref:`nodejs_web_app`
* :ref:`running_redis_service`
* :ref:`running_ssh_service`
* :ref:`running_couchdb_service`
* :ref:`postgresql_service`
* :ref:`mongodb_image`
