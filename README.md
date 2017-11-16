# Set-up the environment on the Google Cloud Platform (GCP)
Running Jupyter for Machine Learning on Google Cloud Platform 
## Configuration in GCP Console
### Create VM Instance
Fill in
* Name
* Zone
* Machine type
* OS Ubuntu 16.04 LTS
* Firewalls: Enable HTTP, HTTPS
* Boot drive: Uncheck Delete Bootdrive
Click create, start VM
### VM Network Settings
Go to VPC Network, External IP Adresses. Click Reserve Static Address
Enter Name, select your Region and VM (Attached to)

Go to VPC Network, Firewall rules. Click CREATE FIREWALL RULE
Enter Name, Source IP ranges (0.0.0.0/0), Protocols and ports (tcp:6006, tcp:8888)

Click Create
## Prepare VM
### Open SSH session
In compute engine, VM instances, connect SSH in new browser Window
### Install Docker
```
sudo apt-get update
sudo apt-get install -y docker.io
sudo docker version
sudo docker info
sudo service docker status
```
### Get a ready Machine Learning image 
Use from Github the *All-in-one Docker image for Deep Learning* https://github.com/floydhub/dl-docker
It contains:
* Ubuntu 14.04
* CUDA 8.0 (GPU version only)
* cuDNN v5 (GPU version only)
* Tensorflow
* Caffe
* Theano
* Keras
* Lasagne
* Torch (includes nn, cutorch, cunn and cuDNN bindings)
* iPython/Jupyter Notebook (including iTorch kernel)
* Numpy, SciPy, Pandas, Scikit Learn, Matplotlib
* OpenCV
* A few common libraries used for deep learning
Install on your VM
```
sudo docker pull floydhub/dl-docker:cpu
```
Run
```
sudo docker run -it -p 8888:8888 -p 6006:6006 -v /sharedfolder:/root/sharedfold
er floydhub/dl-docker:cpu bash
```
Start Jupyter server
```
run_jupyter.sh
```
### Accessing Jupyter
In your browser connect to the static IP of the VM xx.xxx.xx.xx:8888
