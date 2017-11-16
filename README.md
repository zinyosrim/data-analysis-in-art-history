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
Enter Name, Source IP ranges (0.0.0.0/0), Protocols and ports (tcp:80-8888)

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
```
### Get the Anaconda Image 
Install and run on your VM
```
sudo docker run -p 8888:8888 -it  continuumio/anaconda3:v2_gcp
```
Start Jupyter Server
```
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root
``` 
You will get a message like:
```
The Jupyter Notebook is running at: http://0.0.0.0:8888/?token=546277c6b8858664455c24101f0ceec9e53e87374359c61f
```

### Accessing Jupyter
Copy the piece :8888/?token..... and append to your static IP.
In your browser connect to the static IP of the VM xx.xxx.xx.xx:8888/?token=546277c6b8858664455c24101f0ceec9e53e87374359c61f
