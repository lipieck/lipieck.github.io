---
title: How to set up a Factorio Server easily with docker-compose
tags: [Docker, Linux]
style: fill
color: success
description: Factorio server setup
---

Since I have had a bit of trouble with setting up a Factorio server on my linux server. I decided to write a guide on how to set up such a server on a linux machine

## 1. Set up Docker
If you have installed Docker Desktop for Linux, you should have everything required for running the docker image. However, the process is a bit different on machines that you are running in the command line. [You can chceck the installation of Docker Engine in such cases.](https://docs.docker.com/engine/install/) To verify that you have docker installed, you can run the following:
```
sudo docker run hello-world
```
If succesful, it will output a Hello World message, indicating that you have Docker installed.
## 2. Get the Factorio-server git repository

Run the following command:
```
git clone https://github.com/factoriotools/factorio-docker.git
```
This will clone the actual factorio server to your linux machine and create a folder where your docker compose files will be stored. Then navigate to the created directory using:
```
cd factorio-docker/docker
```
Then create the folder where your configuration files will be stored using:
```
sudo mkdir -p /opt/factorio
```
## 3. Run the Docker Compose 
Finally, run the docker-compose to build your server:
```
sudo docker-compose up -d
```

After its done, you will want to shut it down, because it's not properly configured yet. We will have to edit its configuration files to provide the rest of necessary details.
Do so by first checking the name of the docker-compose environment and then stopping it using the following two commands

```
sudo docker-compose ls
sudo docker-compose stop [name of the service (most likely factorio-docker)]
```

## 4. Configure the factorio server settings

Navigate to your Factorio server installation to finish the setup:

```
cd /opt/factorio/config
```
Then edit the configuration file using:
```
sudo nano server-settings.json
```

The lines you will want to change are the following:
```
  "name": "_Name of your server[PLACEHOLDER]_",
  "description": "_Description of your server in the server browser[PLACEHOLDER]_",

  "_comment_visibility": [
    "public: Game will be published on the official Factorio matching server",
    "lan: Game will be broadcast on LAN"
  ],
  "visibility": {
    "public": _false/true_,
    "lan": _false/true_
  },

  "_comment_credentials": "Your factorio.com login credentials. Required for games with visibility public",
  "username": "_YOUR FACTORIO.COM USERNAME_",
  "password": "_YOUR FACTORIO.COM PASSWORD_",

  "_comment_token": "Authentication token. May be used instead of 'password' above.",
  "token": "_YOUR FACTORIO.COM TOKEN_",

  "game_password": "_PASSWORD USERS WIL HAVE TO ENTER WHEN THEY WANT TO JOIN_",

  "_comment_require_user_verification": "When set to true, the server will only allow clients that have a valid Factorio.com account",
  "require_user_verification": _true/false_,

```

To explain a bit further: If you want to run your server, you either need to enter your Username + Password, OR Username + token. Also if you want people who don't have a legitimate version of Factorio to join in or dont want to have a Factorio.com account to join in, set the user verification to False. Then, you will most likely need to set the server to LAN as well.

## 5. Re-run the server

Finally, you can restart the server:
```
sudo docker-composer start [name of your factorio server service]
```
To make sure that the  server has started succesfully, you can check the internal logs for errors using:
```
sudo docker-composer logs [name of your factorio server service]
```