---
layout: post
title: Setting up the blog using Jekyll and Github
---
Copied from
https://www.kaggle.com/kambarakun/how-to-start-with-python-on-colfax-cluster

0. First of all
This kernel is the tutorial to explore and visualize datasets and train Convolutional Neural Network (CNN) on keras.
I'm not good at English. So, please post a comment if there are any unknown points:)
Additionally, this kernel is unfinished, still writing. I will do my best!
This kernel is getting better little by little. Many thanks to all of the comments.
1. Environment construction
In this kernel, you will mainly compute with python on Colfax Cluster.
The datasets (test, train, additional) had extracted and placed in /data/kaggle/ directory on Colfax Cluster.
So, you don't have to download datasets on your local machine.
Of course, you can download them while reading this kernel for killing time.
Datasets are here: https://www.kaggle.com/c/intel-mobileodt-cervical-cancer-screening/data
Note:
You can use extracted datasets on kaggle's kernel too.
But I recommend using Colfax Cluster from the point of computing speed and making your original submission.
1-1. Setting ssh connection to Colfax Cluster
Sign up to Colfax Cluster: https://www.kaggle.com/c/intel-mobileodt-cervical-cancer-screening#Intel-Tutorial
Reference to ssh connection:https://access.colfaxresearch.com/?p=connect
Remember:
chmod 600 ~/Downloads/colfax-access-key-****
1-2. Build enviroment after connect to Colfax Cluster by ssh colfax
Make own environment, install opencv, etc.
ssh colfax
conda create --name test_env jupyter
source activate test_env
conda install numpy pandas opencv scikit-learn matplotlib tensorflow keras jupyter
1-3. Configure Jupyter Notebook, port and password (Thanks to everyone commented)
For avoid port collision and access by other user's access.
Select port (recommended)
Select port number, not likely to make collision. Default is 8888.
If port collides, another port will be used (like 8888 -> 8889).
It's a hassle, so use unique port.
If you are not familiar with network port configurations, I think ephemeral ports (49152 - 65535) are useful.
Here is the script to choose random ephemeral ports. Of course, you can choose your favorite number in 49152 - 65535.
python -c "import random; ports = range(49152, 65535 + 1); random.shuffle(ports); print ports[0]"

Make Password hash (recommended)
Run the bellow command, input password twice, then you get hashed-password.
python -c "from notebook.auth import passwd; print passwd()"
# e.g.) => sha1:237ca8abda58:9aef98cbcbae988caab4b9f86084ff22a1b2b373

Generate and edit config file
Generate config file (~/.jupyter/jupyter_notebook_config.py)
jupyter notebook --generate-config

Edit via vi like this
vi ~/.jupyter/jupyter_notebook_config.py
....
# c.NotebookApp.password = u''
c.NotebookApp.password = u'sha1:237ca8abda58:9aef98cbcbae988caab4b9f86084ff22a1b2b373'
....
# c.NotebookApp.port = 8888
c.NotebookApp.port = 1234

If you are not familiar with vi, use the bellow scripts (need to edit)
echo "c.NotebookApp.password = u'sha1:237ca8abda58:9aef98cbcbae988caab4b9f86084ff22a1b2b373'\n" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.port = 1234\n" >> ~/.jupyter/jupyter_notebook_config.py

If you missed something, you can regenerate (over-write) config file.
jupyter notebook --generate-config

Note: If your setting port makes port collision unfortunately, another port will be used.
1-4. Connect to Colfax Cluster by ssh tunneling, and run Jupyter Notebook
Before runnig Jupyter Notebook, once logout.
logout

And, runnig Jupyter Notebook via ssh tunneling
ssh -L 8890:localhost:8890 colfax -Y
source activate test_env
jupyter notebook --no-browser

Note: The window (ran command) should be kept opened!
Note: You can change port this step (Special thanks to Sriracha's comment)
ssh -L 8890:localhost:8890 colfax -Y
source activate test_env
jupyter notebook --no-browser --port=4321
1-5. Access to Jupyter Notebook on Colfax Cluste by your local machine's browser
Access by your web browser (e.g. Google Chrome) on your local machine (e.g. Windows, Mac...)

http://localhost:1234/ or http://127.0.0.1:1234/ (if you can't)
