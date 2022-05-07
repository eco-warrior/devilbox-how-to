# devilbox-how-to
This is a simple guide for devilbox installation

> **Note:**
>
> For Linux OSes based on Debian releases.
>
> My OS: MXLinux

## Contents

1. [Required Software](#required-software)
2. [Install Required Software](#install-required-software)
3. [Install Devilbox](#install-devilbox)
4. [Configure Devilbox](#configure-devilbox)
5. [Using Devilbox](#using-devilbox)
4. [Tips and Commands](#tips-and-commands)

## Required Software
- Docker
- Docker-Compose
- Devilbox

## Install Required Software

* Install using the repository
* Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

2.1  Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```console
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
```
2.2 Add Docker’s official GPG key:

```console
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

2.3 Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below.
```console
echo \ "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \ $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

2.4 Install Docker Engine
This procedure works for Debian on x86_64 / amd64, armhf, arm64, and Raspbian.
Update the apt package index, and install the latest version of Docker Engine, containerd, and Docker Compose, or go to the next step to install a specific version:
```console
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose docker-compose-plugin
```

Verify that Docker Engine is installed correctly by running the hello-world image.
```console
sudo docker run hello-world
```

## Install Devilbox
* The devilbox does not need to be installed. The only thing that is required is its git directory. To download that, open a terminal and copy/paste the following command.

```console
- git clone https://github.com/cytopia/devilbox
```

3.1 Create .env file
Inside the cloned Devilbox git directory, you will find a file called env-example. This file is the main configuration with sane defaults for Docker Compose. In order to use it, it must be copied to a file named .env. (Pay attention to the leading dot).

```console
- sudo cp env-example .env
```
The .env file does nothing else then providing environment variables for Docker Compose and in this case it is used as the main configuration file for the Devilbox by providing all kinds of settings (such as which version to start up).

## Configure Devilbox

Inside .env file you can change htdocs dir, php version, httpd module, mysql version.

4.1 For htdocs you need to edit the line:

```
HOST_PATH_HTTPD_DATADIR=./data/www
HOST_PATH_HTTPD_DATADIR=/home/USER/path/path
```

4.2 To change php version just comment/uncomment the version you need to use.

```
#PHP_SERVER=php-fpm-5.2
#PHP_SERVER=php-fpm-5.3
#PHP_SERVER=php-fpm-5.4
#PHP_SERVER=php-fpm-5.5
#PHP_SERVER=php-fpm-5.6
#PHP_SERVER=php-fpm-7.0
#PHP_SERVER=php-fpm-7.1
#PHP_SERVER=php-fpm-7.2
#PHP_SERVER=php-fpm-7.3
#PHP_SERVER=php-fpm-7.4
#PHP_SERVER=php-fpm-8.0
PHP_SERVER=php-fpm-8.1
#PHP_SERVER=php-fpm-8.2
```

4.3 For httpd module you need to comment/uncomment the module you want to use as httpd

```
#HTTPD_SERVER=apache-2.2
#HTTPD_SERVER=apache-2.4
HTTPD_SERVER=nginx-stable
#HTTPD_SERVER=nginx-mainline
```

4.4 For mysql server version again comment/uncomment your version:

```
#MYSQL_SERVER=mysql-5.5
#MYSQL_SERVER=mysql-5.6
#MYSQL_SERVER=mysql-5.7
#MYSQL_SERVER=mysql-8.0
#MYSQL_SERVER=percona-5.5
#MYSQL_SERVER=percona-5.6
#MYSQL_SERVER=percona-5.7
#MYSQL_SERVER=percona-8.0
#MYSQL_SERVER=mariadb-5.5
#MYSQL_SERVER=mariadb-10.0
#MYSQL_SERVER=mariadb-10.1
#MYSQL_SERVER=mariadb-10.2
#MYSQL_SERVER=mariadb-10.3
#MYSQL_SERVER=mariadb-10.4
#MYSQL_SERVER=mariadb-10.5
MYSQL_SERVER=mariadb-10.6
#MYSQL_SERVER=mariadb-10.7
#MYSQL_SERVER=mariadb-10.8
```

4.5 Save your .env file and then run:

```console
sudo docker-compose kill <- to kill all containers
sudo docker-compose up -d httpd php mysql <- to download and start your new containers
```
Open http://localhost to see if everything are working

These instructions will get you through the bootstrap phase of creating and
deploying samples of containerized applications with Docker Compose.

## Using Devilbox

4.1 Upload a project your projects path
>**Note**:
> When you create a project always create a folder htdocs inside your project and put the www files there.
##### Screenshot:
![screenshot](github-logo.png)

4.2 Go to Virtual Hosts tab at your localhost
##### Screenshot:
![screenshot](github-logo.png)

4.3 Open and edit /etch/hosts:
```
sudo nano /etc/hosts
127.0.0.1 vhost
```

4.4 Open your browser and type xenf.loc to see that is working.
##### Screenshot:
![screenshot](github-logo.png)


## Tips and Commands

##### tips:

Always using 127.0.0.1 when you are putting MySQL Hostname on installs.

To avoid Wordpress FTP credentials just put this on your wp-config.php
```
define( 'FS_METHOD', 'direct' );
```

##### commands:
```
docker-compose up <- start all containers
```
```
docker-compose kill <- kill all containers
```
```
docker-compose up httpd php mysql <- start containers at foreground
```
```
docker-compose up -d httpd php mysql <- start containers at backround
```

## Links
Fully documentation can be found here:
https://devilbox.readthedocs.io/en/latest/index.html
