# Azure Machine Learning service Hands-On all for TensorFlow

This sample shows how to use Azure Machine Learning (AML) service using TensorFlow along with the entire development lifecycle (explore data, train, tune, and publish).

You can get [MNIST](http://yann.lecun.com/exdb/mnist/) dataset (**train.tfrecords**, **test.tfrecords**) in this example by running the following code.

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
- Login your VM. Remove azure-ml-admin-cli extension as follows. (This extension is already installed on DSVM and prevents you from running ```az login``` command.)

```
sudo -i az extension remove --name azure-ml-admin-cli
```

- Create conda virtual environment and activate.

```
conda create -n myenv -y Python=3.6
conda activate myenv
```

- Install required packages in your conda environment (You must run in your conda env.)

```
# install AML SDK
# this also installs notebook in your conda env
pip install azureml-sdk[notebooks]

# install notebook integration for conda
conda install nb_conda

# install required packages for development
conda install -y matplotlib scikit-learn

# these extensions are needed for showing AML run history widget in notebook
jupyter nbextension install --py --user azureml.train.widgets
jupyter nbextension enable --py --user azureml.train.widgets
```

## 2. Create AML Workspace

Create new "Machine Learning services workspace" using [Azure Portal](https://portal.azure.com/)    

## 3. Make Sure to Install ACI Provider in Your Azure Subscription

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

- Copy url for notebook in the console output, and open corresponding port on VM or set SSH tunnel on your desktop to access notebook.   
  For instance, the following picture is the SSH tunnel setting in "putty" terminal client.    
  ![SSH Tunnel settings with putty](https://i1155.photobucket.com/albums/p551/tsmatsuz/20180216_SSH_Tunnel_zpsjfahueum.jpg)

- Open your notebook url using web browser.

- Create new notebook by selecting "Python 3" (which is your current environment)

<br />
<br />
Now you're ready to start !

See my post "[7 Reasons to Consider Azure Machine Learning Services](https://tsmatz.wordpress.com/2018/11/20/azure-machine-learning-services/)" for details.
