## Prerequisites

If you are using pip, install a recent version of nodejs/npm. For example, install it on Linux (Debian/Ubuntu) using:
```bash
sudo apt-get install nodejs npm
```
## Installation

pip, npm:

```bash
python3 -m pip install jupyterhub

npm install -g configurable-http-proxy

python3 -m pip install jupyterlab notebook  # needed if running the notebook servers in the same environmentv

jupyterhub -h

configurable-http-proxy -h
```

If you plan to run notebook servers locally, you will need to install JupyterLab or Jupyter notebook:

```bash
python3 -m pip install --upgrade jupyterlab

python3 -m pip install --upgrade notebook
```
If needed to add users
```bash
adduser USERNAME e.g adduser rauf
````

## Start the Hub server

```bash
jupyterhub
```
