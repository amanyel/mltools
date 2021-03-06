# mltools

[![PyPI version](https://badge.fury.io/py/mltools.svg)](https://badge.fury.io/py/mltools)

Tools for fast prototyping of object detection and classification solutions on DG imagery.
Relies heavily on popular machine learning (ML) toolkits such as scikit-learn and deep
learning toolkits such as keras. The intent is to use mltools to experiment with algorithms;
when these are mature, they can be baked into GBDX tasks and deployed at scale on [GBDX](developer.digitalglobe.com/gbdx).  

mltools also includes a collection of auxiliary tools necessary for pre- and post- ML processing.
These are:

+ data_extractors: get pixels and metadata from DigitalGlobe imagery; uses [geoio](https://github.com/digitalglobe/geoio);
+ features: functions to derive features from pixels;
+ geojson_tools: functions to manipulate geojson files;
+ crowdsourcing: interface with Tomnod to obtain training/test/target data and to write machine output to Tomnod DB.

Example code can be found in /examples. The examples can be used as a guideline to create object detection/classification
solutions which involve one or more of the following steps:

1. retrieve training, test and target data from the Tomnod database;
2. train the algorithm;
3. test the algorithm on the test data and compute accuracy metrics;
4. deploy the algorithm on the target data for detection or classification;
5. write results back to the Tomnod database;
6. bake algorithm into GBDX task and deploy on GBDX.

Steps 1 or 5 can be omitted if data is available from a source other than Tomnod or
if results do not need to be written back to Tomnod.
Note that instructions on step 6 are NOT yet included in the examples (but they will arrive shortly).
In the meantime, please see [here](http://gbdxdocs.digitalglobe.com).


## Installation/Usage

For Ubuntu, install conda with the following commands (choose default options at prompt):

      wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
      bash Miniconda2-latest-Linux-x86_64.sh


For OS X, install conda with the following commands (choose default options at prompt):

      wget https://repo.continuum.io/miniconda/Miniconda2-latest-MacOSX-x86_64.sh
      bash Miniconda2-latest-MacOSX-x86_64.sh

Then run:

      bash

so that modifications in your .bashrc take effect.

Create a conda environment:

      conda create -n env python ipython numpy scipy gdal libgdal=2 git psycopg2 ephem

Activate the environment:

      source activate env

Upgrade pip (if required):

      pip install pip --upgrade

Install mltools:

      pip install mltools

Optional: you can install the current version of the master branch with:

      pip install git+https://github.com/DigitalGlobe/mltools

Keep in mind that the master branch is constantly under development.

If installation fails for some of the dependencies, (try to) install them with conda:

      conda install <dependency_name>

and then retry:

      pip install mltools

The examples require imagery which can be ordered and downloaded from GBDX using [gbdxtools](http://github.com/digitalglobe/gbdxtools). You can install gbdxtools within the conda environment with:

      pip install gbdxtools

If you have any trouble with the installation of gbdxtools, refer to the readme of the gbdxtools repo.

You can now copy the scripts found in /examples in your project directory or create your own.
Keep in mind that the imagery has to be in your project folder and it should have the same name as the image_name
property in the geojson.

To exit your conda virtual environment:

      source deactivate


## Development

Activate the conda environment:

      source activate env

Clone the repo:

      git clone https://github.com/kostasthebarbarian/mltools

      cd mltools

Install the requirements:

      pip install -r requirements.txt

Please follow [this python style guide](https://google.github.io/styleguide/pyguide.html). 80-90 columns is fine.

To exit your conda virtual environment:

      source deactivate

### Create a new version

To create a new version:

      bumpversion ( major | minor | patch )
      git push --tags

Then upload to pypi.


## Comments

[Here](https://docs.google.com/drawings/d/1tKSgFMp0lLd7Abne8CdOhb1PbdJfgCz5x9XkLwDeET0/edit?usp=sharing) is a slide my initial ideas on mltools. The vision is to use the solutions created with mltools as part of a Crowd+Machine system along the lines of [this document](https://docs.google.com/document/d/1hf82I_jDNGc0NdopXxW9RkbQjLOOGkV4lU5kdM5tqlA/edit?usp=sharing).
