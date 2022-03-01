# Set Up for AML CLI

Before you start exercises, you must provision your working environment as follows.

## 1. Setup your Virtual Machine

Here we setup Ubuntu environment for running Azure Machine Learning CLI (version 2.0 or above).

- Create Ubuntu 18.04 LTS virtual machine resource in [Azure Portal](https://portal.azure.com/).

> Note : In this example, we use TensorFlow 1.x. It needs Python version 3.6, and you cannot then use Python 3.7 or later.

- Install Azure CLI version 2.15 or above as follows. (See [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux) for details.)

```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

> Note : To see the installed version, run ```az --version```.

- Install AML CLI version 2 or above as follows.

```
az extension add --name ml --version 2.1.2
```

> Note : "**Data Science Virtual Machine (DSVM) on Ubuntu**" in Microsoft Azure will also include the pre-configured Azure CLI and AML CLI.

- In this tutorial, we run examples in IPython notebook.<br>
  Please make sure that Python 3.6 is installed on Ubuntu. (As I have mentioned above, you cannot use python 3.7 or above to run TensorFlow 1.x.)

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

- Install Jupyter notebook as follows.

```
pip3 install jupyter
```

- Install required packages for this tutorial. (Use "tensorflow-gpu" if using GPU VM.)

```
pip3 install matplotlib tensorflow==1.15
```

## 2. Create Azure ML Workspace

Create new "Machine Learning" resource in [Azure Portal](https://portal.azure.com/) .

> Note : Please specify the location (region), in which you can run GPU virtual machine.<br>
> See [Exercise04](./exercise04_train_remote.ipynb) for details. (Please request quota for GPU AML VM, if you don't have any GPU quotas in your Azure subscription.)

## 3. Clone this repo

Clone this repo in your working environment.

```
git clone https://github.com/tsmatz/azureml-tutorial
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

*back to [index](https://github.com/tsmatz/azureml-tutorial/)*
