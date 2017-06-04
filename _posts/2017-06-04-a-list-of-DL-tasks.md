---
layout: post
title: A List of Deep Learning Tasks
---
- Kaggle Competition on Cervical Cancer Screening: https://www.kaggle.com/c/intel-mobileodt-cervical-cancer-screening

- Stanford Image Recognition Master Class: http://cs231n.github.io/

- Running Caffe on AWS using Docker: http://tleyden.github.io/blog/2014/10/25/running-caffe-on-aws-gpu-instance-via-docker/

1. Set up a caffe classification on INTEL COLFEX
- half successful
- set up a ssh on mac to connect to INTEL COLFEX using
    And, runnig Jupyter Notebook via ssh tunneling
    
      ssh -L 8890:localhost:8890 colfax -Y
      
      source activate test_env
      
      jupyter notebook --no-browser
      
- caffe is installed and jupyter notebook examples can be opened
- but the examples cannot be run for various reasons. Memory problem, read-only directory, etc.
- caffe needs python 2 environment to be set up
    conda create -n ipykernel_py2 python=2 ipykernel
    source activate ipykernel_py2    # On Windows, remove the word 'source'
    python -m ipykernel install --user
    conda install numpy pandas opencv scikit-learn matplotlib tensorflow keras jupyter scikit-image
- Colfex can send jobs to queue in the different nodes
    https://access.colfaxresearch.com/?p=compute
    Submit a Shell Command
        This will execute the command lscpu on the first available node:

        [u3842@c001 ~]$ echo lscpu | qsub
        520.c001BashCopy
        Once the job enters the queue, qsub will return the job ID, in this example 520.c001. Make a note of the job number, which in this example is 520.

        The job will be scheduled for execution, and, once it completes, you will find files STDIN.o520 and STDIN.e520. Here

        STDIN is the job name (by default, equal to STDIN for jobs submitted via the pipe |)
        520 is the job number
        STDIN.o520 is the standard output stream of the job
        STDERR.e520 is the standard error stream of the job
        [u3842@c001 ~]$ cat STDIN.o520 | grep Model name
        Model name:            Intel(R) Xeon Phi(TM) CPU 7250 @ 1.40GHz



2. Install Caffe on Mac <- no GPU
  - CUDA tutorial, driver and sample is installed successfully
  - cuDNN is a folder? not sure how to use it
  - Mac does not have any NVIDIA chip. Video card is AMD Radeon HD 6490M 256 MB
  
3. Run python image classification on INTEL Jupyter (need any feature extraction?)
  - How to start with python on INTEL COLFEX CLUSTER
    https://www.kaggle.com/kambarakun/how-to-start-with-python-on-colfax-cluster
  - successfully run sample code
  
4. Set up TensorFlow on INTEL
  - Not yet done
  
5. Try using INTEL deep learning tool. (Monday)
  - successfuly installed after installing DOCKER EDGE and sign in to DOCKERHUB
