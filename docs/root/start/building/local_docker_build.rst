
.. _install_sandboxes_local_docker_build:

Building an Envoy Docker image
==============================

The following steps guide you through building your own Envoy binary, and
putting that in a clean Ubuntu container.

**Step 1: Build Envoy**

Using ``envoyproxy/envoy-build`` you will compile Envoy.
This image has all software needed to build Envoy. From your Envoy directory:

.. code-block:: console

  $ pwd
  src/envoy
  $ ./ci/run_envoy_docker.sh './ci/do_ci.sh bazel.release'

That command will take some time to run because it is compiling an Envoy binary and running tests.

If your system has limited resources, or you wish to build without running the tests, you can
also build as follows:

.. code-block:: console

  $ pwd
  src/envoy
  $ ./ci/run_envoy_docker.sh './ci/do_ci.sh bazel.release.server_only'


For more information on building and different build targets, please refer to :repo:`ci/README.md`.

.. warning::

   These instructions for building Envoy use
   `envoyproxy/envoy-build-ubuntu <https://hub.docker.com/r/envoyproxy/envoy-build-ubuntu/tags>`_ image.
   You will need 4-5GB of disk space to accommodate this image.

   This script runs as effective root on your host system.

**Step 2: Build image with only Envoy binary**

In this step we'll build an image that only has the Envoy binary, and none
of the software used to build it.:

.. code-block:: console

  $ pwd
  src/envoy/
  $ docker build -f ci/Dockerfile-envoy -t envoy .

Now you can use this ``envoy`` image to build the any of the sandboxes if you change
the ``FROM`` line in any Dockerfile.

This will be particularly useful if you are interested in modifying Envoy, and testing
your changes.
