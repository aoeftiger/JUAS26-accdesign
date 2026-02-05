# Joint Universities Accelerator School: Accelerator Design Workshop

The [JUAS](https://www.esi-archamps.eu/juas-presentation/) features an [accelerator design workshop](https://esi-archamps.eu/juas-courses/#1636455686368-8e28251f-fd39). This repository provides the lattice design jupyter notebook, which contains the setup and exercises to design a particle collider using the [xsuite](https://xsuite.readthedocs.io/en/latest/) simulation framework.

This repository provides an `xsuite` configuration for running jupyter notebooks, locally inside a [docker](https://docker.com/) container or on [mybinder.org](https://mybinder.org/).

Launch an interactive binder instance here:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/aoeftiger/JUAS26-accdesign/v1.0)

The published docker image is found here:

[![Docker](https://shields.io/docker/image-size/aoeftiger/juas26-accdesign?logo=docker)](https://hub.docker.com/r/aoeftiger/juas26-accdesign)

## Running the container
The docker container can be run on the command line via

### linux / macOS

    JUPYTER_TOKEN=jc docker run -p 8880:8888 -e JUPYTER_TOKEN -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS='-R' -v $HOME:/home/jovyan/home/ aoeftiger/juas26-accdesign

### Windows

using `cmd.exe`:

    set JUPYTER_TOKEN=js && docker run -p 8880:8888 -e JUPYTER_TOKEN -v %USERPROFILE%:/home/jovyan/home/ aoeftiger/juas26-accdesign

or using PowerShell:

    $env:JUPYTER_TOKEN='js'; docker run -p 8880:8888 -e JUPYTER_TOKEN -v ${env:USERPROFILE}:/home/jovyan/home/ aoeftiger/juas26-accdesign

where

 - `JUPYTER_TOKEN=jc` sets the token (password) for entering the jupyter server
 - `-p 8880:8888` forwards the jupyter server port from inside the container to your outside system (change the first port `8880` to your liking)
 - `-v $HOME:/home/jovyan/home` binds your home directory to inside the docker container such that you can save and load notebooks.

Next you can open your browser and load the page [https://localhost:8880/?token=jc](https://localhost:8880/?token=jc) to connect to the running jupyter lab server.

## Building locally
The docker container for this repository can be built locally by running on the command line

    docker build -t aoeftiger/juas26-accdesign .

## Troubleshooting
If you face permission issues with accessing your home directory from within the container, you might want to provide your user ID and group ID explicitly to the container as a solution.

On linux, check your user and group IDs via the CLI command `$ id` and use these values when running the container as above but with the additional arguments:

    [...] --user root -e NB_UID=<your user id> -e NB_GID=<your group id> [...]

Add these comments before the mount instruction `-v [...]`.
