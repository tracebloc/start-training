# Jupyter notebook for Start Training
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Data scientist tool to create and run experiment with required model and training plan .


## Pre-requisite
### 1. Install Ananconda
```shell
wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh 

bash Anaconda3-2020.11-Linux-x86_64.sh -b -p -y 

source ~/.bashrc 
```
### 2. Create an environment and activate it
```shell
conda create -n dsenvironemnt python=3.8 

conda activate dsenvironemnt 
```
### 3. Install required package
```shell
pip install -r requirement.txt
```
### 4. Install tensorflow and keras
```shell
pip install tensorflow==2.6.0
pip install keras==2.6.0

```
#### In case of mac m1 machine

Follow this link to install tensorflow: https://caffeinedev.medium.com/how-to-install-tensorflow-on-m1-mac-8e9b91d93706

or

Enter following commands
```shell
conda install -c apple tensorflow-deps
pip install tensorflow-macos
pip install tensorflow-metal
pip uninstall -y numpy
pip uninstall -y setuptools
pip install numpy
pip install setuptools
```
### 4. Install Jupyter Notebook
```shell
conda install jupyter notebook

pip install jupyter
```
### 5. Move to Directory
```shell
cd federated-xray-datascientist
```
### 6. Start Jupyter Notebook
```shell
jupyter notebook
```


## Testing Jupyter Notebook
In order to start and test experiment, go through step by step guide [Start Training](https://traceblocdocsdev.azureedge.net/category/start-training)

## 📜 License
This project is licensed under the MIT License - see the [LICENSE.txt](LICENSE.txt) file for details.


## 📞 Support
For additional support or questions, please refer to our documentation or contact the Tracebloc support team at `support@tracebloc.io`.
