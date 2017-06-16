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

make all
make test
make runtest
