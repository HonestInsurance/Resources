[<img src="https://github.com/HonestInsurance/Resources/blob/master/branding/HonestInsurance-hor-blue.png?raw=true" width="250">](https://www.honestinsurance.net)

-----------------------

Setup, configuration and as-build-documentation for API server and full vaidating Ethereum (Geth) node.

-----------------------

# 1 - Infrastructure
Amazon Web Services (AWS) - Elastic Compute Cloud (EC2)
* 2 x OS - Ubuntu 18.04.2 LTS instances
  * apinode@api-node-01
  * ethnode@eth-node-01
* 2 x Elastic IPs
  * api-ip-adr
  * eth-ip-adr

-----------------------

# 2 - Basic setup and configuration of servers

**1. Change server name to [api|eth]-node-01 [[Source](https://linuxize.com/post/how-to-change-hostname-on-ubuntu-18-04/)]:**

`$ sudo hostnamectl set-hostname [api|eth]-node-01`

`$ sudo vi /etc/cloud/cloud.cfg`

Change line and set `preserve_hostname: true`

Verify change of server name: `$ sudo hostnamectl`

**2. Create server user [api|eth]node:**

Create user and provide temporary password:

`$ sudo adduser [api|eth]node`

Add user to sudo group:

`$ sudo usermod -aG sudo [api|eth]node`


**3. Remove password requirement for sudo command**
Edit the sudoers file:

`$ sudo visudo`

Change lane and set `%sudo ALL=(ALL) NOPASSWD: ALL`

**4. Create rsa public/private key pair and copy authorised ssh key for ssh access**

`$ su [api|eth]node`

`$ cd $HOME`

`$ mkdir .ssh`

`$ chmod 600 .ssh`

`$ cd .ssh`

Create a rsa key pair and use default settings without providing a password [[Source](https://www.debian.org/devel/passwordlessssh)]

`$ ssh-keygen`

Create authorized keys file and copy public ssh key of connecting devices into file

`$ touch authorized_keys`

`chmod 600 authorized_keys`

**5. Remove configured temporary password**

`sudo passwd -d [api|eth]node`

**6. Delete default user [ubuntu] and home directory created during server initialisation**

`sudo deluser --remove-home ubuntu`

**7. Create 'ssh jump script' called shd for easy assess to all servers**

`$ sudo vi /usr/local/bin/shd` 

```
#!/bin/bash
if [ -z "$1" ]
  then
    echo "No destination ['api', 'eth', 'sim'] supplied!"
    exit
fi

if [ $1 = "api" ]; then
    ssh apinode@api.honestinsurance.net

elif [ $1 = "eth" ]; then
    ssh ethnode@eth.honestinsurance.net

elif [ $1 = "sim" ]; then
    ssh simnode@sim.honestinsurance.net
fi
```

`$ sudo chmod 777 /usr/local/bin/shd`

**8. Update all server packages**

`$ sudo apt update`

`$ sudo apt upgrade`

-----------------------

# 3 - Server: api-node-01 - Install dotnet core runtime

1. As there is no development happening on the server only the runtime version needs to be installed. 
2. All available versions of dotnet and installation instructions are available **[here](https://dotnet.microsoft.com/download/dotnet-core)**
3. Select the latest LTS [Long term support] version of .NET Core available
4. Select the **Runtime** package manager instructions for **Linux x64**
5. Select **Ubuntu 18.04 - x64** as the Linux Distribution

```
$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
$ sudo dpkg -i packages-microsoft-prod.deb

$ sudo add-apt-repository universe
$ sudo apt-get install apt-transport-https
$ sudo apt-get update
$ sudo apt-get install aspnetcore-runtime-2.1
```

-----------------------

# 4 - Server: api-node-01 - Install Nginx and configure a server

**[Installation Instructions and documenation](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-nginx?view=aspnetcore-2.1#install-nginx)**

## 4.1 Install Nginx

`$ sudo apt-get install nginx`

Start the Nginx service:

`$ sudo service nginx start`

Edit the nginx configuration file:

`$ sudo vi /etc/nginx/sites-available/default`

```
server {
    listen 80;
    server_name  api.honestinsurance.net api.honest.tech;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Verify the syntax of the changes with:

`sudo nginx -t`

Reload the changes:

`sudo nginx -s reload`

## 4.2 Create application service definition file to manage kestrel service by systemd

**[Installation Instructions and documenation](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-nginx?view=aspnetcore-2.1#create-the-service-file)**

The server is setup to forward requests made to http://<serveraddress>:80 on to the ASP.NET Core app running on Kestrel at http://127.0.0.1:5000. However, Nginx isn't set up to manage the Kestrel process. systemd can be used to create a service file to start and monitor the underlying web app. systemd is an init system that provides many powerful features for starting, stopping, and managing processes.

Create a service definition file:

`$ sudo vi /etc/systemd/system/kestrel-ApiService.service`

```
[Unit]
Description=Api Service providing api layer to connect with Ethereum Blockchain contracts

[Service]
WorkingDirectory=/home/apinode/ApiService
ExecStart=/usr/bin/dotnet /home/apinode/ApiService/ApiService.dll
Restart=always
RestartSec=10  # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=ApiService
User=apinode
Environment=ASPNETCORE_ENVIRONMENT=Ubuntu_Development

[Install]
WantedBy=multi-user.target
```

Enable the kestrel service to be managed by systemd (leave passwords blank):

`$ sudo systemctl enable kestrel-ApiService.service`

When changing the ‘kestrel-ApiService.service’ file use the following command to reload the changes:

`$ sudo systemctl daemon-reload`

Useful commands to start, stop, monitor the kestrel service:

```
$ sudo systemctl start kestrel-ApiService.service
$ sudo systemctl status kestrel-ApiService.service
$ sudo journalctl -fu kestrel-ApiService.service
$ sudo journalctl -n all -fu kestrel-ApiService.service
$ sudo systemctl stop kestrel-ApiService.service
```

Create simple scipts to start, stop, monitor service:
```
cd /usr/local/bin
sudo touch start status stop logs
sudo chmod 777 start status stop logs

echo '#!/bin/bash' >> start
echo 'sudo systemctl start kestrel-ApiService.service' >> start

echo '#!/bin/bash' >> stop
echo 'sudo systemctl stop kestrel-ApiService.service' >> stop

echo '#!/bin/bash' >> status
echo 'sudo systemctl status kestrel-ApiService.service' >> status
```

`$ sudo vi /usr/local/bin/logs`

```
#!/bin/bash
if [ -z "$1" ]
  then
    journalctl -fu kestrel-ApiService.service
    exit
fi

if [ $1 = "all" ]; then
    journalctl -n all -fu kestrel-ApiService.service
fi
```

-----------------------

# 5 - Server: api-node-01 - Install SSL certificates on ubuntu server using certbot

**[Certbot installation instructions and documentation](https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx)**

## 5.1 Install certbot

`$ sudo apt-get update`

`$ sudo apt-get install software-properties-common`

`$ sudo add-apt-repository universe`

`$ sudo add-apt-repository ppa:certbot/certbot`

`$ sudo apt-get update`

`$ sudo apt-get install certbot python-certbot-nginx `


## 5.2 Configure the domains for which certificates should be installed in the nginx config file

Edit the config file and specify the server_name URL endpoints:

`$ sudo vi /etc/nginx/sites-available/default`

```
server {
    listen 80;
    server_name  api.honestinsurance.net api.honest.tech;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Verify syntax of configuration file with:

`sudo nginx -t`

Reload the configuration file with:

`sudo nginx -s reload`

## 5.3 Install the certificates

As part of the installation of the ssl certificates choose the option to forward all HTTP traffic by default to HTTPS. This will update the previously configured ngix config file accordingly.

`$ sudo certbot --nginx --register-unsafely-without-email`

## 5.4 Renew the certificates

Display status about currently certbot installed certificates:

`$ sudo certbot certificates`

Renew all certificates that are due to expire soon:

`$ sudo certbot renew`

Test the automatic reneal feature of certbot:

`$ sudo certbot renew --dry-run`

-----------------------

# 6 - Server: api-node-01 - Deploy API dotnet core package to server remotely

The below script needs to be run on the machine on which the development of the api service is commencing.

`$ sudo vi /usr/local/bin/deploy`

`$ sudo chmod 777 /usr/local/bin/deploy`

```
#!/bin/bash
RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m'

# Set source code directory for deployment
CODE_HOME=$HOME/GitHub/Api-Services/ApiService

# Connect and stop web service on remote server
echo -n "Stopping web service process on remote server  .................  "
ssh apinode@api.honestinsurance.net "\stop"
echo -e "${GREEN}Stopped ${NC}"

# Create deployment package locally
echo -n "Creating .Net Core App 2.1 release package  ....................  "
( cd $CODE_HOME && dotnet publish -f netcoreapp2.1 -c Release &>/dev/null )
echo -e "${GREEN}Done ${NC}"

# Deploy release package on remot server by copying the release files
echo -n "Deploying release package on remote server  ....................  "
scp -P 22 -r $CODE_HOME/bin/Release/netcoreapp2.1/publish/* apinode@api.honestinsurance.net:/home/apinode/ApiService &>/dev/null
echo -e "${GREEN}Done ${NC}"

# Start web service on remot server again
echo -n "Starting web service process on remote server  .................  "
ssh apinode@api.honestinsurance.net "\start"    
echo -e "${GREEN}Started ${NC}"
```

Note: This script assumes the API source code directoy to be at `$HOME/GitHub/Api-Services`. In addition this script creates a .Net Core app targeting the LTS version `2.1`. The deployment directory on the target server is `/home/apinode/ApiService`. Ensure this folder exists prior running the deployment script.

The license file `ServiceStackLicense.txt` for ServiceStack is not being deployed as part of this script and needs to be copied manually into the `ApiService/config/` folder on the server.

The file `ApiService/config/config.json` contains the configuration parameters of the api service and can be modified on the server without reqiring a re-deployment of the service. However the service needs to be restarted with the commands `stop` and `start` to reload the new configuration settings.

-----------------------

# 7 - Server: eth-node-01 - Install nginx and SSL certificates on ubuntu server using certbot

## 7.1 Install Nginx

Follow the steps as [outlined above](#41-install-nginx) and specify the below configuration file:

`$ sudo vi /etc/nginx/sites-available/default`

```
server {
    listen 80;
    server_name  eth.honestinsurance.net eth.honest.tech rinkeby.honestinsurance.net rinkeby.honest.tech;
    location / {
        proxy_pass http://0.0.0.0:8545;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_cache_bypass $http_upgrade;
    }
}
```

**Important:** Ensure to use the above configuration file for nginx as it differs from the one used earlier. In particular DO NOT USE THE LINE BELOW IN THE FILE (otherwise Geth rejects the incoming requests):

`proxy_set_header Host $host;`

## 7.2 Install SSL certificates

Follow the steps as [outlined above](#5---server-api-node-01---install-ssl-certificates-on-ubuntu-server-using-certbot) by using the earlier configured nginx configuration file.

-----------------------

# 8 - Server: eth-node-01 - Install Geth and configure scripts

**[Installation instructions and documentation](https://github.com/ethereum/go-ethereum/wiki/Installation-Instructions-for-Ubuntu)**

## 8.1 Install Geth

`$ sudo apt-get install software-properties-common`

`$ sudo add-apt-repository -y ppa:ethereum/ethereum`

`$ sudo apt-get update`

`$ sudo apt-get install ethereum`

## 6.2 Scripts to start, stop and monitor the Geth node

Create simple scipts to start, stop, monitor service:
```
cd /usr/local/bin
sudo touch start status stop logs
sudo chmod 777 start status stop logs
```

`$ sudo vi /usr/local/bin/start`

```
#!/bin/bash
echo ""
echo "Starting Geth node for Rinkeby ..."
nohup geth --syncmode "fast" --rinkeby --rpcapi eth,web3,net --rpc --rpcport "8545" --rpcaddr "127.0.0.1" --rpccorsdomain  "*" --cache=1014 >> $HOME/rinkeby.log &
echo "Geth node started ..."
echo ""
```

`$ sudo vi /usr/local/bin/status`

```
#!/bin/bash
echo ""
echo "GETH process"
echo "------------"
SEARCH_TERM='geth'
ps -ef | grep -m 1 $SEARCH_TERM
echo ""
echo "Last log file entries"
echo "----------------------"
tail -n 5 $HOME/rinkeby.log
echo ""
```

`$ sudo vi /usr/local/bin/stop`

```
#!/bin/bash
echo ""
PID=`pgrep -f geth`
if [ -z "$PID" ]
  then
    echo "No geth process is currently running ..."
    exit
fi
echo "Stopping the Geth process ..."
kill -INT $PID
echo "Geth process stopped ..." 
echo ""
```

`$ sudo vi /usr/local/bin/logs`

```
#!/bin/bash
tail -f $HOME/rinkeby.log
```

## 6.3 Sync the node with the `start` command

To start the geth node and trigger the synchronisation of the node use the `$ start` script. To speed up the initial syncronisation of the node it is advisable to reserve 3.5GB or more RAM and 2 or more vCPUs to the server for this initial process.

Note 1: While the initial syncronisation is running do not interrup this process until it's complete as flag `--syncmode "fast"` only works if the node is being synchronised from scratch.

Note 2: This command synchronises the Rinkeby chain.

Note 3: The location of the Blockchain files as well as keys and node details is `$HOME/.ethereum`.