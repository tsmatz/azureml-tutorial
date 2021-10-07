# Azure Machine Learning Step-by-Step Tutorial (with TensorFlow 1.x)

This sample shows generic flows of Azure Machine Learning (formerly, Azure Machine Learning service) using TensorFlow version 1.x along with the entire development lifecycle (exploration, train, tune, and publishing).

By running [here](https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/examples/how_tos/reading_data/convert_to_records.py), you can take [MNIST](http://yann.lecun.com/exdb/mnist/) dataset (**train.tfrecords**, **test.tfrecords**) , which is used in this example. Let's put these files into ```data``` folder.

- [Exercise01 : Prepare Config Settings](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise01_prepare_config.ipynb)
- [Exercise02 : Prepare Data](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise02_prepare_data.ipynb)
- [Exercise03 : Just Train in Your Working Machine](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise03_train_simple.ipynb)
- [Exercise04 : Train on Remote GPU Virtual Machine](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise04_train_remote.ipynb)
- [Exercise05 : Distributed Training](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise05_train_distributed.ipynb)
- [Exercise06 : Experimentation Logs and Outputs](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise06_experimentation.ipynb)
- [Exercise07 : Hyperparameter Tuning](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise07_tune_hyperparameter.ipynb)
- [Exercise08 : Publish as a Web Service](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise08_publish_model.ipynb)

> Note : In this hands-on, we manually configure TensorFlow 1.x. You can also use built-in curated environments in Azure Machine Learning.

Before starting, you must provision your working environment as follows :

## 1. Setup your Virtual Machine

Azure Machine Learning provides its own notebook environment in AML studio UI.<br>
However, you can setup you own environment with Azure Machine Learning SDK in Ubuntu, Mac OS, etc.

In this tutorial, we'll setup our environment with Anaconda in Ubuntu virtual machine on Azure.

- Create "Data Science Virtual Machine (DSVM) on Ubuntu" resource in [Azure Portal](https://portal.azure.com/).<br>
  In DSVM, Conda (Anaconda) has already installed and configured, but you can also build your own environment from scratch. (DSVM also includes Azure ML CLI.)

- Create conda virtual environment and activate (enter into) this environment as follows. (Here I named "myenv" as follows.)<br>
TensorFlow 1.x needs Python version 3.6. (You cannot use Python 3.7 or later.)

```
conda create -n myenv -y Python=3.6
conda activate myenv
```

- Install Jupyter notebook in your current conda environment (```myenv```).

```
# Install jupyter notebook
pip install notebook

# Install notebook integration for conda
conda install nb_conda
```

- Install required Python packages in your conda environment as follows.<br>
Azure Machine Learning (AML) provides extension packages as well as core package (```azureml-core```). For instance, if you want to run Automated machine learning in AML, you should install additional automl extension package (```azureml-train-automl```) as well.<br>
In this tutorial, we use AML interactive widget's extension (```azureml_widgets```), which is installed as Jupyter notebook extension and used in Exercise 06, and AML train core extension (```azureml-train```) which is used in Exercise 07. (Run ```jupyter nbextension list``` to see the installed Jupyter extensions.)

```
# Install AML SDK Core
pip install azureml-core

# Install AML interactive widgets extension
pip install azureml-widgets

# Install AML train extension (including HyperDrive package)
pip install azureml-train

# Install AML dataset extension
pip install azureml-dataset-runtime

# Install required packages for this tutorial
# (use "tensorflow-gpu" if using GPU VM)
conda install -y matplotlib tensorflow==1.15
```

## 2. Create Azure ML Workspace

Create new "Machine Learning" resource in [Azure Portal](https://portal.azure.com/) .

> Note : It's not mandatory, but it's better to specify the location (region), in which you can run GPU virtual machine.
> See [Exercise04](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/blob/master/notebooks/exercise04_train_remote.ipynb) for details. (Please request quota for GPU VM, if you don't have any GPU quotas.)

## 3. Clone this repo

Clone this repo in your working environment.

```
git clone https://github.com/tsmatz/azureml-tutorial-tensorflow-v1
```

## 4. Start Jupyter Notebook

- Start Jupyter Notebook within your conda environment. This will show the access url, such as ```http://localhost:8888/tree?token=xxxxxxxxxx```.

```
jupyter notebook
```

- Set SSH tunnel (port forwarding) on your working desktop to access notebook URL.<br>
  For instance, the following is the SSH tunnel setting on "PuTTY" terminal client in Windows. (You can use ```ssh -L``` option in Mac OS.)    
  ![SSH Tunnel settings with putty](https://tsmatz.github.io/images/github/azure-ml-tensorflow-complete-sample/20191225_SSH_Tunnel.jpg)

- Copy URL (```http://localhost:8888/?token=...```) for notebook in the console output and open this address with web browser.

- Create a new ipy notebook by selecting your current conda environment.

<br />
<br />
Now you're ready to start !

See my post "[Azure Machine Learning Key Features for AI Engineers](https://tsmatz.wordpress.com/2018/11/20/azure-machine-learning-services/)" for summarizing key features about Azure Machine Learning.

*Tsuyoshi Matsuzaki @ Microsoft*
