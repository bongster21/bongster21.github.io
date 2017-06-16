---
layout: post
name: Install Caffe on Mac Sierra
---

General dependencies

brew install -vd snappy leveldb gflags glog szip lmdb
# need the homebrew science source for OpenCV and hdf5
brew tap homebrew/science
brew install hdf5 opencv

Remaining dependencies, with / without Python

# with Python pycaffe needs dependencies built from source
brew install --build-from-source --with-python -vd protobuf
brew install --build-from-source -vd boost boost-python
# without Python the usual installation suffices
brew install protobuf boost


cp Makefile.config.example Makefile.config
# Adjust Makefile.config (for example, if using Anaconda Python, or if cuDNN is desired)

uncomment #CPU_ONLY := 1
uncomment #WITH_PYTHON_LAYER := 1

------------------
Error: cblas missing
Solution : install cblas

brew install --fresh -vd openblas
uncomment in Makefile.config:
BLAS_INCLUDE := /path/to/your/blas

BLAS_LIB := /path/to/your/blas

------------------

Error: missing pyconfig

Somehow system python cannot be used because pyconfig.h does not exist! (exist only in python-dev)
So, do:
brew install python 

and update in Makefile.config:
PYTHON_INCLUDE := /usr/local/lib/python2.7/site-packages/numpy/core/include/ /usr/local/Cellar/python/2.7.10/Frameworks/Python.framework/Versions/2.7/include/python2.7

------------------

make all

Speed: for a faster build, compile in parallel by doing make all -j8 where 8 is the number of parallel threads for compilation

make test
make runtest
