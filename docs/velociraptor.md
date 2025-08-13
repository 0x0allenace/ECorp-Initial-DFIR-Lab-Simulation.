# Velociraptor Setup & Clients Integration

## Introduction
Velociraptor is an endpoint visibility and collection tool designed for digital forensics and incident response (DFIR).  
This guide will walk you through installing the Velociraptor server, integrating it with client virtual machines.

## Overview
This guide walks through the installation and configuration of **Velociraptor** on an Ubuntu virtual machine (VM).  
The process is the same whether you are using **Proxmox**, **VirtualBox**, or **VMWare**. 

## Prerequisites

Before installing Velociraptor:

**Assign a Static IP Address** to the Ubuntu VM.

Ensure **`net-tools`** is installed, as it is required to manage networking configurations.

### Install `net-tools`

sudo apt install net-tools

![vr01](/images/vr1.png)

### Run ifconfig to confirm the IP address and the adaptor name.

ifconfig

![vr02](/images/vr2.png)

### Run ip r to confirm the gateway IP address.
ip r

![vr03](/images/vr3.png)

### Set the static ip address using the command below.

sudo ifconfig enp6s18 10.0.2.8 netmask 255.255.255.0

![vr04](/images/vr4.png)

### Set the default gateway.
sudo route add default gw 10.0.2.1 enp6s18

![vr05](/images/vr5.png)

### Download Velociraptor from the github page using the wget command below.

wget https://github.com/Velocidex/velociraptor/releases/download/v0.73/velociraptor-v0.73.1-linux-amd64

![vr06](/images/vr6.png)

## Run ls -la to confirm the download and then change the permission to allow us to execute it.

ls -la
chmod 764 velociraptor-v0.73.1-linux-amd64

Create a directory for Velociraptor.

sudo mkdir /opt/velociraptor

Create the server configuration file.

sudo ./velociraptor-v0.73.1-linux-amd64 config generate -i 

### Make the following selections during the interactive configuration.

![vr07](/images/vr7.png)

### Finish creating the configuration files with the options shown below.

![vr08](/images/vr8.png)

### Confirm the config files were written by going running the command below.

ls -la /opt/velociraptor

![vr09](/images/vr9.png)

We need to edit the server .yaml by using the text editor nano to change the GUI IP address to the IP address of the Velociraptor server we just installed.

sudo nano /opt/velociraptor/server.config.yaml

### Scroll down to GUI bind IP address and change the IP address from 127.0.0.1 to the IP of the server, in my case it is 10.0.2.8.

![vr10](/images/vr10.png)

### Save the file.

Create a debian package for the server by using the command below.

sudo ./velociraptor-v0.73.1-linux-amd64 —config /opt/velociraptor/server.config.yaml debian server --binary velociraptor-v0.73.1-linux-amd64  

![vr11](/images/vr11.png)

### Now that the package is created we can run it.

sudo dpkg -i velociraptor_server_0.73.1_amd64.deb

![vr12](/images/vr12.png)

The package created a new group, system user, and the velociraptor process. We can confirm the service is running by using the command below.

systemctl status velociraptor_server.service

![vr13](/images/vr13.png)

### We can now access the server via of the web interface by navigating to https://10.0.2.8:8889

![vr14](/images/vr14.png)

### Log in with the username and password you chose while configuring the server.

![vr15](/images/vr15.png)

### We have successfully set up the server; however, we have not set up any clients yet.

![vr16](/images/vr16.png)

To create a client we need to download the Windows Velociraptor binary. We can download it from the github similar to the way we downloaded the Linux Velociraptor binary.

wget https://github.com/Velocidex/velociraptor/releases/download/v0.73/velociraptor-v0.73.1-windows-amd64.exe

![vr17](/images/vr17.png)


Repackage the binary by importing in the client config file we created earlier.

sudo ./velociraptor-v0.73.1-linux-amd64 config repack --exe velociraptor-v0.73.1-windows-amd64 /opt/velociraptor/client.config.yaml vraptorclient.exe 

![vr18](/images/vr18.png)

### Run ls -la to confirm the file was created.

ls -la

![vr19](/images/vr19.png)

As seen above the .exe file was created. 

### To move the .exe to our Windows VM we can set up a webserver using python’s webserver module.

sudo python3 -m http.server 1337

![vr20](/images/vr20.png)

### Go to your windows machine and open a browser and navigate to http:10.0.2.8:1337

![vr21](/images/vr21.png)

### Open PowerShell as administrator and navigate to the Downloads folder.

![vr22](/images/vr22.png)


### Execute the file using this command:
.\vraptorclient.exe service install

![vr23](/images/vr23.png)

### Access the Velociraptor web interface by navigating to https://10.0.2.8:8889.

![vr24](/images/vr24.png)
