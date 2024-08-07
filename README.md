# Hyperledger Fabric Prerequisites Setup

1) Create a new sudo user
   
   add new user “fabric”
   
   ``` bash
   sudo adduser fabric
   ```
   
   Add the user “fabric” to the Sudo groups
   ``` bash
   sudo usermod -aG sudo fabric
   ```
   
   Login to “fabric” user
   ``` bash
   su fabric
   ```
   
   Test the sudo access
   ``` bash
    sudo ls
   ```

3) Install cURL
   ``` bash
   sudo apt-get update
   sudo apt-get install curl
   ```
   
5) Install Docker CE (Community Edition )

   First download and then install it using below commands. <br>
   ```bash
   https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/docker-ce_18.06.3~ce~3-0~ubuntu_amd64.deb
 
   sudo dpkg -i docker-ce_18.06.3~ce~3-0~ubuntu_amd64.deb
   ```
6) Install Docker Compose
   ```bash
   Run below commands to setup Docker compose.
 
   sudo apt-get install python-pip
 
   pip --version
 
   sudo pip install docker-compose

   ```

   To use docker commands it requires root privileges. Instead of using sudo for all the docker commands, add the user to docker group
   ``` bash
   sudo usermod -aG docker fabric
   ```
   
![Screenshot from 2024-04-29 16-12-17](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/4bbd2273-c717-4d69-866f-b999fce32bc9)

   Logout using exit command and log in again. Check the groups' user is part of, using id -nG command.

   Test the Installation
 
   Pull the hello-world image from Docker Hub and run a container:
   ``` bash
   docker run hello-world
   ```

![Screenshot from 2024-04-29 16-24-48](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/6aad260b-29a2-42e1-991f-14ed83e836cf)

5) Install Golang
   ``` bash
   Install the golang package
   curl -O https://storage.googleapis.com/golang/go1.11.linux-amd64.tar.gz

   Extract the package
   tar xvf go1.11.linux-amd64.tar.gz

   ```
![Screenshot from 2024-04-29 16-25-22](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/a472e4f7-2b5f-4916-a599-bb54b7b4b8a4)

   Set the GOPATH using command
   ``` bash
   export GOPATH=$HOME/go
   export PATH=$PATH:$GOPATH/bin

   ```
   
![Screenshot from 2024-04-29 16-37-36](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/cd29a0f9-ad8d-40d0-b58e-44c424d1de05)

   check go version
  
![Screenshot from 2024-04-29 16-31-03](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/9ac11685-78cd-4b57-b2e5-b48208548325)

6)  Nodejs and npm
    Download the installation script using curl
    ``` bash
    curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
    ```
    Run the script under sudo
    ``` bash
    sudo bash nodesource_setup.sh
    ```
    Install the nodejs
    ``` bash
    sudo apt-get install nodejs
    ```
    With nodejs, npm also get installed. Check their version
    ``` bash
    node -v
    npm -v
    ```
  8) install  python
     ``` bash
        sudo apt-get install python
     ```
   
![Screenshot from 2024-04-29 16-38-43](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/c16b26ea-6f61-422b-b422-3ac8bd137437)

# Hyperledger installation
 Determine the directory where you want to download the fabric samples. Open the directory in terminal and run the below command
 ``` bash
 curl -sSL http://bit.ly/2ysbOFE | bash -s -- 2.4.4 1.5.3
```
![Screenshot from 2024-05-06 15-57-10](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/c0363df4-ef5a-4fa1-9037-8ffd57551594)

![Screenshot from 2024-05-06 15-57-36](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/f49c5f82-ef25-4f4e-9cd5-c633917f0c03)

# Create Peers and Channel
  Go to fabric-samples folder by using below command.
  ``` bash
   cd fabric-samples
  ```
  Go to test-network folder by using below command.
  ``` bash
    cd test-network
  ```
  Run below command to start your test-network
  ``` bash
   sudo ./network.sh up
  ```


![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/72c53f39-2e09-4f12-bd04-c0d2d12b79e6)


![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/433cac18-83c2-4442-8550-a2a10b9e84ca)

 Run below command to check docker containers.
  ``` bash
  sudo docker ps
  ```
 This shows you three docker containers
 1. One for Org1 peer node
 2. One for Org2 peer node
 3. One for Orderer

![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/f699aaa9-6646-4c0f-bda4-4a4248684a52)

 When you start the network, you will also not get any channel by default. You can check the channel by using below command.
 ``` bash
  sudo docker exec peer0.org1.example.com peer channel list
 ```

![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/1afbf792-6e55-4f6d-a739-102807dc9f2f)

 Create new channel by using below command.
 ``` bash
   sudo ./network.sh createChannel -c testchannel
 ```

![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/c66efc22-fdd5-4e32-991d-18a636a2c8af)
 To verify this channel creation, run below command on both the peers.
   ``` bash
   sudo docker exec peer0.org1.example.com peer channel list
   sudo docker exec peer0.org2.example.com peer channel list
  ```
![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/07149bc1-1c70-49bc-9aa8-90acf5dcae93)
 Step 5: To stop the network, you need to run below command.
   ``` bash
   sudo ./network.sh down
   ```
 ![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/71ca972f-67d3-41a2-9e5a-1c21dd9ce366)

# Create CA
 Go to fabric-samples folder by using below command.
 ```bash
  cd fabric-samples
 ```
 Go to test-network folder by using below command.
 ``` bash
 cd test-network
 ```
 Run below command to start test-network and create CA container for each organization ( one for orderer, one for org1 peer and one for org2 peer)
 ``` bash
 sudo ./network.sh up -ca
 ```


![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/eae71048-149b-4d91-a0e2-ad91f33e7d9c)



![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/85a5207f-2703-4506-84a8-b4fadfb382b5)

![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/f62fdadf-d67e-4c08-8c0f-bf213b94ebed)

 Create new channel by using below command.
``` bash
 sudo ./network.sh createChannel -c testchannel2
```
![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/598c3fda-e647-4c86-aaa4-81c53e78ecbc)

 To stop the network, you need to run below command.
 ``` bash
 sudo ./network.sh down
 ```
![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/77cbd3a1-fd70-4cc8-94d1-052dc67675fd)


# Create Couchdb
 Go to fabric-samples folder by using below command.
 ``` bash 
 cd fabric-samples
 ```
 Go to test-network folder by using below command.
 ``` bash
 cd test-network
 ```
 Run below command to start the network and create couchDB containers as well.
 ``` bash
 sudo ./network.sh up -s couchdb
 ```


![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/66fb0d6e-40f0-4251-97dc-5b753bfe3f9c)


![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/9df332b5-1581-48fc-be39-9a606985df7a)

 Create new channel by using below command.
 ``` bash
 sudo ./network.sh createChannel -c testchannel1
 ```
![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/aad1e4e4-4e77-4f04-9bee-9a169bfb92b9)


![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/1ce58d02-400b-42e7-9603-a27c73570bc3)

To stop the network, you need to run below command.
``` bash
   sudo ./network.sh down
```
![image](https://github.com/RupeshKumar4511/Hyperledger-Project/assets/149661006/8657d090-9d09-424e-b1dd-92a2d5d71b1d)


# Reference :
Youtube Channel : Code Eater

