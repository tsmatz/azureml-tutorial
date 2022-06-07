# Azure Machine Learning Tutorial (Python SDK / YAML)

This example shows you generic AI / ML workflow through lifecycle - exploration, train, tune, and publishing - with Azure Machine Learning (AML) API.<br>
(Here I assume **TensorFlow version 1.x** for AI / ML framework.)

There exist 2 options to run Azure Machine Learning (AML) API - Python SDK and CLI/YAML.

<ins>**CLI / YAML (v2)**</ins>

- [Exercise01 : Login Azure](./cli_yaml/exercise01_login_azure.ipynb)
- [Exercise02 : Prepare Data](./cli_yaml/exercise02_prepare_data.ipynb)
- [Exercise03 : Just Train in Your Working Machine](./cli_yaml/exercise03_train_simple.ipynb)
- [Exercise04 : Train on Remote GPU Virtual Machine](./cli_yaml/exercise04_train_remote.ipynb)
- [Exercise05 : Distributed Training](./cli_yaml/exercise05_train_distributed.ipynb)
- [Exercise06 : Track Logs and Metrics](./cli_yaml/exercise06_experimentation.ipynb)
- [Exercise07 : Hyperparameter Tuning](./cli_yaml/exercise07_tune_hyperparameter.ipynb)
- [Exercise08 : Publish as a Web Service](./cli_yaml/exercise08_publish_model.ipynb)
- [Exercise09 : ML Pipeline (MLOps Integration)](./cli_yaml/exercise09_ml_pipeline.ipynb)

<ins>**Python SDK v1**</ins>

- [Exercise01 : Prepare Config Settings](./notebooks/exercise01_prepare_config.ipynb)
- [Exercise02 : Prepare Data](./notebooks/exercise02_prepare_data.ipynb)
- [Exercise03 : Just Train in Your Working Machine](./notebooks/exercise03_train_simple.ipynb)
- [Exercise04 : Train on Remote GPU Virtual Machine](./notebooks/exercise04_train_remote.ipynb)
- [Exercise05 : Distributed Training](./notebooks/exercise05_train_distributed.ipynb)
- [Exercise06 : Track Logs and Metrics](./notebooks/exercise06_experimentation.ipynb)
- [Exercise07 : Hyperparameter Tuning](./notebooks/exercise07_tune_hyperparameter.ipynb)
- [Exercise08 : Publish as a Web Service](./notebooks/exercise08_publish_model.ipynb)
- [Exercise09 : ML Pipeline (MLOps Integration)](./notebooks/exercise09_ml_pipeline.ipynb)

> Note : You can also use raw REST API for involing AML API.

## How to Set up

### 1. Create Azure ML Workspace resource

Create new "Machine Learning" resource in [Azure Portal](https://portal.azure.com/) .

> Note : We need GPU instance in Exercise04. Please specify the location (region) for machine learning resource, in which you can run GPU virtual machine.<br>
> See [Exercise04](./notebooks/exercise04_train_remote.ipynb) for details. (Please request quota for GPU AML VM, if you don't have any GPU quotas in your Azure subscription.)

### 2. Create Virtual Machine for running AML API

In Exercise03, we use TensorFlow 1.x and you cannot then use Python 3.7 or later.<br>
In order to use Python 3.6, here I use **Ubuntu Server 18.04 LTS in Microsoft Azure** for client, in which Python 3.6 is already installed.

- Create Ubuntu Server 18.04 LTS virtual machine resource in [Azure Portal](https://portal.azure.com/).

- Please make sure that Python 3.6 is installed on Ubuntu. (As I have mentioned above, you cannot use Python 3.7 or above to run TensorFlow 1.x.)

```
# Check version
python3 -V
### # Set python3.6 as default python command (Here I assume /usr/bin/python3.6)
### sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1
````

- Install and upgrade pip3 as follows.

```
sudo apt-get update
sudo apt-get install -y python3-pip
sudo -H pip3 install --upgrade pip
```

- In this tutorial, we run all exercises in IPython notebook.<br>
  Install Jupyter as follows.

```
pip3 install jupyter
```

- Install the required packages for Exercise03. (Use "tensorflow-gpu" instead, when using GPU VM.)

```
pip3 install matplotlib tensorflow==1.15
```

**Choose the following settings (3A or 3B), depending on which API (Python SDK or CLI/YAML) you use.**

### 3A [CLI/YAML v2] Set up Azure ML CLI

For running AML CLI/YAML, install Azure Machine Learning CLI extension version 2.0 or above as follows.

- Install Azure CLI (version 2.15 or above) as follows. (See [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux) for details.)

```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

> Note : To see the installed Azure CLI version, run ```az --version```.

- Install AML CLI extension as follows.

```
az extension add --name ml
```

> Note : In this example, I have used CLI version 2.4.1. When you install a specific version, please run ```az extension add --name ml --version 2.4.1```.

### 3B [Python SDK v1] Set up Azure ML SDK v1

For running AML Python SDK v1, install Python SDK version 1 and depending other packages as follows.

Azure Machine Learning (AML) provides core package (```azureml-core```) and as well as extension packages. Depending on tasks, you should install addtional extensions. (For instance, if you want to run automated machine learning in AML, you should install automl extension package (```azureml-train-automl```) as well.)

In this tutorial, we use AML interactive widget's extension (```azureml_widgets```) used in Exercise 06, and AML train core extension (```azureml-train```) used in Exercise 07, and pipeline extensions (```azureml-pipeline-core``` and ```azureml-pipeline-steps```) used in Exercise 09.<br>
Install the required Python packages as follows.

```
# Install AML SDK Core
pip3 install azureml-core

# Install AML interactive widgets extension
pip3 install azureml-widgets

# Install AML train extension (including HyperDrive package)
pip3 install azureml-train

# Install AML dataset extension
pip3 install azureml-dataset-runtime

# Install AML pipeline extension
pip3 install azureml-pipeline-core azureml-pipeline-steps
```

> Note : AML widget's extension is installed as Jupyter notebook extension.<br>
> Run ```jupyter nbextension list``` to see the installed Jupyter extensions.

### 4. Clone this repo

Clone this repository in your working environment.

```
git clone https://github.com/tsmatz/azureml-tutorial
```

### 5. Start Jupyter Notebook

- Start Jupyter notebook as follows. (Please re-login to take effect for "jupyter" path.)<br>
  This will show the access url in console, such as ```http://localhost:8888/tree?token=xxxxxxxxxx```.<br>
  (The default port is 8888.)

```
jupyter notebook
```

- Connect to Ubuntu server with SSH tunnel (port forwarding) from your working desktop in order to access notebook URL.<br>
  For instance, the following is the SSH tunnel setting on "PuTTY" terminal client in Windows. (You can use ```ssh -L``` option in Mac OS.)<br>
  ![SSH Tunnel settings with putty](https://tsmatz.github.io/images/github/azure-ml-tensorflow-complete-sample/20191225_SSH_Tunnel.jpg)

- Copy the notebook URL (```http://localhost:8888/?token=...```) in the console output (see above) and open this address with your web browser.



See my post "[Azure Machine Learning Introduction and Key Features](https://tsmatz.wordpress.com/2018/11/20/azure-machine-learning-services/)" for feature's overview in Azure Machine Learning.

*Tsuyoshi Matsuzaki @ Microsoft*
