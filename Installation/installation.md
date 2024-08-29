# Installation
This is about Installation of the following in **ubuntu 22.04** machine.
#

## NGINX
### Prerequisites
 **Update the system packages**<br>
`sudo apt update`<br>
 `sudo apt upgrade -y` 
 <br>`-y` option is given so there wont be another prompt by the shell  asking for permission either yes or no, implicitly gives yes.

### Proceed with Installation of NGINX
`sudo apt install nginx -y` 
### Start, Enable and Check status
1. starting the service
`sudo systemctl start nginx`
2. enabling the service 
`sudo systemctl enable nginx` #this starts nginx always on systemboot automatically.
3. checking the status 
`sudo systemctl status nginx`

### Output of the `sudo systemctl status nginx` command
![example](/resources/mongo_status.png)
#
## MongoDB
 ### Install prerequired packages for the installation process<br>
` sudo apt install software-properties-common gnupg apt-transport-https ca-certificates -y`
### Install public key to add mongodb repository to your systems source file<br>
```curl -fsSL https://pgp.mongodb.com/server-7.0.asc |  sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor```
### Add MongoDB 7.0 APT repository to the /etc/apt/sources.list.d directory.
```echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list```
### Install mongodb-org package (meta-package) that provides mongodb
`sudo apt install mongodb-org -y`
### Verify installation process
`mongod --version`
### Output of `mongod --version`
![mongod-ver](/resources/mongo_ver.png)
### Start the mongodb service
`sudo systemctl start mongod`
### Status to verify mongodb service
`sudo systemctl status mongod`
### Output of `sudo systemctl status mongod`
![mongod-status](/resources/mongo_status.png)
#
## Node
### Installing Node using NVM
### Install NVM script to your system
`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash`
### To use it source your .bashrc file
`source ~/.bashrc`
### Download any of the available versions of node.
- Check the versions using `nvm list-remote`
- Install the required using `nvm i v20.10.0` ( inplace of `v20.10.0` you can give the version that you require ).
### Output of `nvm i v20.10.0`
![nvm_i_v](/resources/nvm_i_ver.png) 
### Verify installation using `node -v`
![node_v](/resources/node_ver.png)
#
## PM2
### Install PM2 using npm
`sudo npm i pm2@latest -g`<br>
`-g` tells npm to install pm2 globally, so you can use it across all your Node.js applications instead of just the current one
### Verify installation using `pm2 -v`
![pm2_v](/resources/pm2_v.png)