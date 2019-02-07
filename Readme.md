# Azure Machine Learning service Hands-On all for TensorFlow

This sample shows how to use Azure Machine Learning (AML) service using TensorFlow along with the entire development lifecycle (explore data, train, tune, and publish).

You can get [MNIST](http://yann.lecun.com/exdb/mnist/) dataset (**train.tfrecords**, **test.tfrecords**) in this example by running the following code, and put these files into ```data``` folder.

[https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/examples/how_tos/reading_data/convert_to_records.py](https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/examples/how_tos/reading_data/convert_to_records.py)

- [Exercise01 : Prepare Config Settings](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise01_prepare_config.ipynb)
- [Exercise02 : Prepare Datastore](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise02_prepare_datastore.ipynb)
- [Exercise03 : Just Train in Your Working Machine](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise03_train_simple.ipynb)
- [Exercise04 : Train on Remote GPU Virtual Machine](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise04_train_remote.ipynb)
- [Exercise05 : Distributed Training](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise05_train_distributed.ipynb)
- [Exercise06 : Experimentation Logs and Outputs](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise06_experimentation.ipynb)
- [Exercise07 : Hyperparameter Tuning](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise07_tune_hyperparameter.ipynb)
- [Exercise08 : Publish as a Web Service](https://github.com/tsmatz/azure-ml-tensorflow-complete-sample/blob/master/notebooks/exercise08_publish_model.ipynb)

Before starting, you must provision your environment as follows :

## 1. Setup your Virtual Machine and Conda Env

- Create Data Science Virtual Machine (DSVM) on Ubuntu (which also includes Azure ML CLI) using [Azure Portal](https://portal.azure.com/)    
  Here we use DSVM, but you can also build your own environment from scratch.

- Create conda virtual environment and activate as follows.

```
conda create -n myenv -y Python=3.6
conda activate myenv
```

- Install required packages in your conda environment (You must run in your conda env.)    
```azureml-sdk[notebooks]``` installs notebook in your conda env and ```azureml_widgets``` extension (which is used in Exercise06) is enabled in Jupyter. (See installed extension using ```jupyter nbextension list```.)

```
# install AML SDK
pip install azureml-sdk[notebooks]

# install notebook integration for conda
conda install nb_conda

# install required packages for development
# (use "tensorflow-gpu" if using GPU VM)
conda install -y matplotlib tensorflow
```

## 2. Create AML Workspace

Create new "Machine Learning services workspace" using [Azure Portal](https://portal.azure.com/) .    
Please make sure that **you must specify location (region) which supports NC-seriese (K80 GPU) virtual machines in workspace creation**, because workspace location is used when you create AML compute resources (virtual machines) in AML Python SDK. (See [here](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=virtual-machines) for supported regions.)

## 3. Make Sure to Install ACI Provider in Your Azure Subscription

- Remove azure-ml-admin-cli extension on VM as follows. (This extension is already installed on DSVM and prevents you from running ```az login``` command.)

```
sudo -i az extension remove --name azure-ml-admin-cli
```

- Login to Azure using CLI

```
az login
```

- Check to see if ACI provider is already registered

```
az provider show -n Microsoft.ContainerInstance -o table
```

- If ACI is not registered, run the following command. (You should be the subscription owner to run this command.)

```
az provider register -n Microsoft.ContainerInstance
```

## 4. Start Jupyter Notebook

- Start jupyter notebook server in your conda environment.

```
jupyter notebook
```

- Copy url for notebook in the console output, and set SSH tunnel (port forwarding) on your desktop to access notebook.   
  For instance, the following picture is the SSH tunnel setting on "putty" terminal client in Windows. (You can use ```ssh -L``` option in Mac OS.)    
  ![SSH Tunnel settings with putty](https://i1155.photobucket.com/albums/p551/tsmatsuz/20180216_SSH_Tunnel_zpsjfahueum.jpg)

- Open your notebook url (http://localhost:8888/?token=...) using web browser in your desktop.

- Create new notebook by selecting "Python 3" kernel (which is your current conda environment).

<br />
<br />
Now you're ready to start !

See my post "[7 Reasons to Use Azure Machine Learning Services](https://tsmatz.wordpress.com/2018/11/20/azure-machine-learning-services/)" for details.

*Tsuyoshi Matsuzaki @ Microsoft*
