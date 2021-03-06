# CORD-19 Data loader

This python script helps to transform the data set from the [COVID-19 Open Research Dataset Challenge](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge/data)
into a neo4j graph

Maintainer: [Tim](https://github.com/motey)

Version: 0.1.0

Python version: Python3

ThanksTo: https://pypi.org/project/cord-19-tools/

# Usage

## Docker

**Run**

`docker run -it --rm --network host --name cord19 -e CONFIGS_NEO4J='{"host":"localhost"}' covidgraph/data-cord19`

> **NOTE**: For details on the `-e CONFIGS_NEO4J`env variable see https://github.com/covidgraph/motherlode/blob/master/README.md#the-neo4j-connection-string

**Build local image**

From the root directorie of this repo run:

`docker build -t data-cord19 .`

**Run local image**

`docker run -it --rm --network host --name data-cord19 -e CONFIGS_NEO4J='{"host":"localhost"}' data-cord19`

Examples (neo4j runs on the docker linux host machine)

`docker run -it --rm --network host --name data-cord19 -v ${PWD}/dataset:/app/dataset -e CONFIGS_NEO4J='{"host":"localhost"}' data-cord19`

`docker run -it --rm --name data-cord19 -e CONFIGS_NEO4J='{"host":"localhost"}' data-cord19`

My common dev docker call looks like this:

`docker run -it --rm --network host --name data-cord19 -v ${PWD}/dataset:/app/dataset -v ${PWD}/dataloader:/app/dataloader -e CONFIGS_NEO4J='{"host":"localhost"}' data-cord19`

**Envs**

The most important Env variables are:

`ENV`: will be `PROD` or `DEV`


`CONFIGS_NEO4J`: defaults to `{"host":"localhost"}`. The connections details for the database. For details see https://github.com/covidgraph/motherlode/blob/master/README.md#the-neo4j-connection-string

besides that you can set all variables in `dataloader/config.py` via env variable with a `CONFIGS_` prefix. See https://git.connect.dzd-ev.de/dzdtools/pythonmodules/-/tree/master/Configs for more details on how to manipulate the parameters

**Volumes**

`/app/dataset`

Here is the downloaded data set located. You can mount this path with `-v /mylocal/path:/app/dataset` to prevent redownloading of the dataset.

`/app/dataloader`

Here is the python source code located. You can mount this for development or tinkering

## Local

Copy `dataloader/env/DEFAULT.env` to `dataloader/env/DEVELOPMENT.env`:

`cp dataloader/env/DEFAULT.env dataloader/env/DEVELOPMENT.env`

Enter your neo4j connection string at `dataloader/env/DEVELOPMENT.env` into the variable `CONFIGS_NEO4J`:

```env
CONFIGS_NEO4J={"host":"localhost"}
```

Install the requirements with

`pip3 install -r requirement.txt`

run the main.py

`python3 main.py`

# Data

## Scheme

![Datascheme](https://raw.githubusercontent.com/covidgraph/data_cord19/master/docs/datascheme.png)

## Exmaple


![Exmaple Data](https://raw.githubusercontent.com/covidgraph/data_cord19/master/docs/datascheme_example.png)



