# MLR-Legacy-Transformer
[![Build Status](https://travis-ci.org/USGS-CIDA/MLR-Legacy-Transformer.svg?branch=master)](https://travis-ci.org/USGS-CIDA/MLR-Legacy-Transformer)
[![Coverage Status](https://coveralls.io/repos/github/USGS-CIDA/MLR-Legacy-Transformer/badge.svg)](https://coveralls.io/github/USGS-CIDA/MLR-Legacy-Transformer)

Provides services to transform legacy data fields

This project has been built and tested with python 3.6.x. To build the project locally you will need
python 3 and virtualenv installed.
```bash
% virtualenv --python=python3 env
% env/bin/pip install -r requirements.txt
```
To run the tests:
```bash
env/bin/python -m unittest
```

To run the application locally execute the following:
```bash
% env/bin/python app.py
```

The swagger documentation can then be accessed at http://127.0.0.1:5000/api

Default configuration variables can be overridden be creating a .env file. For instance to turn debug on, 
you will want to create an .env with the following:
```python
DEBUG = True
```

The two docker files provided pull the artifact from cida.usgs.gov/artifactory. The build type and version should be 
specfied as build-arg's when building the image. The argument build_type should be 'snapshots' or 'releases'. The 
artfact_version should be the version of the usgs-wma-mlr-legacy-transformer that you want to be used in the docker 
container. The optional build argument, 'listening_port' can be specified and defaults to 7010. 
This port will be exposed by the container. To build within the DOI network, use Dockerfile-DOI and place the DOI 
cert in '/root.crt'. Below is an example of how to build.
```bash
docker build --build-arg artifact_version=0.1.0.dev0 --build-arg build_type=snapshots -t mlr_legacy_transformer -f Dockerfile-DOI .
```

To run, you can specify a bind mount on the host system where you want the exported files written (the src part of the bind). 
Below is an example:
```bash
docker run --publish 5000:7010 mlr_legacy_transformer
```