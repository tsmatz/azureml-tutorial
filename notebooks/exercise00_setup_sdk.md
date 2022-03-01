# Set Up for AML Python SDk

Before you start exercises, you must provision your working environment as follows.

## 1. Setup your Virtual Machine

Azure Machine Learning provides its own notebook environment in AML studio UI.<br>
However, you can setup you own environment with Azure Machine Learning SDK in your favirote environments, such as, Ubuntu, Mac OS, etc.

In this tutorial, we'll setup our environment with Anaconda in Ubuntu virtual machine on Microsoft Azure.

- Create "**Data Science Virtual Machine (DSVM)** on Ubuntu" resource in [Azure Portal](https://portal.azure.com/).<br>
  In DSVM, Conda (Anaconda) has already installed and configured, but you can also build your own environment from scratch.

- Create your own conda virtual environment and activate (enter into) this conda environment. (Here I named "myenv" as follows.)

```
conda create -n myenv -y Python=3.6
conda activate myenv
```

> Note : TensorFlow 1.x needs Python version 3.6, and you cannot then use Python 3.7 or later.

- Install Jupyter notebook in your current conda environment (```myenv```).

```
# Install jupyter notebook
pip install notebook

# Install notebook integration for conda
conda install nb_conda
```

- Install required Python packages in your conda environment as follows.<br>
Azure Machine Learning (AML) provides extension packages as well as core package (```azureml-core```). For instance, if you want to run automated machine learning in AML, you should install additional automl extension package (```azureml-train-automl```) as well.<br>
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

# Install AML pipeline extension
pip install azureml-pipeline-core azureml-pipeline-steps

# Install required packages for this tutorial
# (use "tensorflow-gpu" if using GPU VM)
conda install -y matplotlib tensorflow==1.15
```

## 2. Create Azure ML Workspace

Create new "Machine Learning" resource in [Azure Portal](https://portal.azure.com/) .

> Note : It's better to specify the location (region), in which you can run GPU virtual machine.
> See [Exercise04](./exercise04_train_remote.ipynb) for details. (Please request quota for GPU AML VM, if you don't have any GPU quotas in your Azure subscription.)

## 3. Clone this repo

Clone this repo in your working environment.

```
git clone https://github.com/tsmatz/azureml-tutorial-tensorflow-v1
```

## 4. Start Jupyter Notebook

- Set SSH tunnel (port forwarding) on your working desktop to access notebook URL. (The default port is 8888.)<br>
  For instance, the following is the SSH tunnel setting on "PuTTY" terminal client in Windows. (You can use ```ssh -L``` option in Mac OS.)    
  ![SSH Tunnel settings with putty](https://tsmatz.github.io/images/github/azure-ml-tensorflow-complete-sample/20191225_SSH_Tunnel.jpg)

- Start Jupyter Notebook within your conda environment as follows. This will show the access url, such as ```http://localhost:8888/tree?token=xxxxxxxxxx```.

```
jupyter notebook
```

- Copy URL (```http://localhost:8888/?token=...```) for notebook in the console output and open this address with web browser.

- Make sure that your current conda environment is selected as kernel runtime in IPython (.ipy) notebook.

## 5. Prepare data

Here we use hand-writing digit's dataset ([MNIST](http://yann.lecun.com/exdb/mnist/) dataset) - **train.tfrecords**, **test.tfrecords** - to train in this example.<br>
Run [this script](https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/examples/how_tos/reading_data/convert_to_records.py) and put these files into ```data``` folder.

*back to [index](https://github.com/tsmatz/azureml-tutorial-tensorflow-v1/)*
