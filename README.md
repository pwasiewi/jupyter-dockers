[![Discourse badge](https://img.shields.io/discourse/https/discourse.jupyter.org/users.svg?color=%23f37626)](https://discourse.jupyter.org/c/questions "Jupyter Discourse Q&A")
[![Read the Docs badge](https://img.shields.io/readthedocs/jupyter-docker-stacks.svg)](https://jupyter-docker-stacks.readthedocs.io/en/latest/ "Documentation build status")
[![DockerHub badge](https://images.microbadger.com/badges/version/jupyter/base-notebook.svg)](https://microbadger.com/images/jupyter/base-notebook "Recent tag/version of jupyter/base-notebook")
[![Binder badget](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/jupyter/docker-stacks/master?filepath=README.ipynb "Launch a jupyter/base-notebook container on mybinder.org")

# If notebooks *.ipynb in github do not load, just paste links to https://nbviewer.jupyter.org/

# Run this modified Jupyter docker with added Python packages and a default user: guest (1001,100)
#### Examples 
#### https://github.com/ipython-books/cookbook-2nd-code
#### https://medium.com/@gongsta/how-to-use-pyspark-in-pycharm-ide-2fd8997b1cdd
#### see my notebooks in this repository

docker run -it --rm -p 8888:8888 -p 4040:4040 -e NB_USER=$(whoami) -e NB_UID=$(id -u) -e NB_GID=$(id -g) -v $(pwd):/home/guest/workspace 42n4/all-spark-notebook

#### Jupyter with the graphical gui
docker run -it --rm -p 8888:8888 -p 4040:4040 -e JUPYTER_ENABLE_LAB=yes -e NB_USER=$(whoami) -e NB_UID=$(id -u) -e NB_GID=$(id -g)  -v $(pwd):/home/guest/work 42n4/all-spark-notebook

# Build
### You can pull my docker with all python packages (about 0.5h with a good internet connection)
```
docker pull 42n4/all-spark-notebook   #pull my docker (about 14G in tar - all packages needed for machine learning)
```
### or make it in five steps (about 1 hour on i7) - you can add your packages to Dockerfile:
#### 1
```
git clone https://github.com/pwasiewi/jupyter-dockers
cd jupyter-dockers/base-notebook
# docker build --rm -t 42n4/base-notebook .
docker build --rm -t 42n4/$(basename `pwd`) .
```
#### 2
```
cd ../minimal-notebook
# docker build --rm -t 42n4/minimal-notebook .
docker build --rm -t 42n4/$(basename `pwd`) .
```
#### 3
```
cd ../scipy-notebook
# docker build --rm -t 42n4/scipy-notebook .
docker build --rm -t 42n4/$(basename `pwd`) .
```
#### 4
```
cd ../pyspark-notebook
# docker build --rm -t 42n4/pyspark-notebook .
docker build --rm -t 42n4/$(basename `pwd`) .
```
#### 5
```
cd ../all-spark-notebook
# docker build --rm -t 42n4/all-spark-notebook .
docker build --rm -t 42n4/$(basename `pwd`) .
docker login                            #docker-hub-user-login and pass to hub.docker.com
# docker push 42n4/all-spark-notebook   
docker push 42n4/$(basename `pwd`)      #send to docker-hub-user/docker-name
```

# Jupyter Docker Stacks

Jupyter Docker Stacks are a set of ready-to-run [Docker images](https://hub.docker.com/u/jupyter) containing Jupyter applications and interactive computing tools.

## Quick Start

You can try a [recent build of the jupyter/base-notebook image on mybinder.org](https://mybinder.org/v2/gh/jupyter/docker-stacks/master?filepath=README.ipynb) by simply clicking the preceding link. Otherwise, the two examples below may help you get started if you [have Docker installed](https://docs.docker.com/install/) know [which Docker image](http://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html) you want to use, and want to launch a single Jupyter Notebook server in a container.

The [User Guide on ReadTheDocs](http://jupyter-docker-stacks.readthedocs.io/) describes additional uses and features in detail.

**Example 1:** This command pulls the `jupyter/scipy-notebook` image tagged `17aba6048f44` from Docker Hub if it is not already present on the local host. It then starts a container running a Jupyter Notebook server and exposes the server on host port 8888. The server logs appear in the terminal. Visiting `http://<hostname>:8888/?token=<token>` in a browser loads the Jupyter Notebook dashboard page, where `hostname` is the name of the computer running docker and `token` is the secret token printed in the console. The container remains intact for restart after the notebook server exits.

    docker run -p 8888:8888 jupyter/scipy-notebook:17aba6048f44

**Example 2:** This command performs the same operations as **Example 1**, but it exposes the server on host port 10000 instead of port 8888. Visiting ``http://<hostname>:10000/?token=<token>`` in a browser loads JupyterLab, where ``hostname`` is the name of the computer running docker and ``token`` is the secret token printed in the console.::

    docker run -p 10000:8888 jupyter/scipy-notebook:17aba6048f44

**Example 3:** This command pulls the `jupyter/datascience-notebook` image tagged `9b06df75e445` from Docker Hub if it is not already present on the local host. It then starts an *ephemeral* container running a Jupyter Notebook server and exposes the server on host port 10000. The command mounts the current working directory on the host as `/home/guest/work` in the container. The server logs appear in the terminal. Visiting `http://<hostname>:10000/?token=<token>` in a browser loads JupyterLab, where `hostname` is the name of the computer running docker and `token` is the secret token printed in the console. Docker destroys the container after notebook server exit, but any files written to `~/work` in the container remain intact on the host.

    docker run --rm -p 10000:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/guest/work jupyter/datascience-notebook:9b06df75e445

## Contributing

Please see the [Contributor Guide on ReadTheDocs](http://jupyter-docker-stacks.readthedocs.io/) for information about how to contribute package updates, recipes, features, tests, and community maintained stacks.

## Alternatives

* [jupyter/repo2docker](https://github.com/jupyter/repo2docker) - Turn git repositories into Jupyter-enabled Docker Images
* [openshift/source-to-image](https://github.com/openshift/source-to-image) - A tool for building/building artifacts from source and injecting into docker images
* [jupyter-on-openshift/jupyter-notebooks](https://github.com/jupyter-on-openshift/jupyter-notebooks) - OpenShift compatible S2I builder for basic notebook images

## Resources

* [Documentation on ReadTheDocs](http://jupyter-docker-stacks.readthedocs.io/)
* [Issue Tracker on GitHub](https://github.com/jupyter/docker-stacks)
* [Jupyter Discourse Q&A](https://discourse.jupyter.org/c/questions)
* [Jupyter Website](https://jupyter.org)
* [Images on DockerHub](https://hub.docker.com/u/jupyter)
