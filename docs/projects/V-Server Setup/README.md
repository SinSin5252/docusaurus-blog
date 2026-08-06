# V-Server Setup

A simple web server built using Nginx. This project documents the setup and deployment of a website on a Linux server.

The project covers:

- Connecting to a remote Linux server using SSH
- Setting up Git access via SSH
- Installing and configuring Nginx
- Deploying a website to the webserver

## Table of Contents

- [Establish a Connection to the Target Server](#establish-a-connection-to-the-target-server)
    - [1. Generate an SSH Key](#1-generate-an-ssh-key)
    - [2. Copy the Public Key to the Server](#2-copy-the-public-key-to-the-server)
    - [3. Connect Using the SSH Key](#3-connect-using-the-ssh-key)
    - [4. Disable Password Authentication](#4-disable-password-authentication)
- [Establish Git Access via SSH](#establish-git-access-via-ssh)
    - [1. Generate an SSH Key for Git](#1-generate-an-ssh-key-for-git)
    - [2. Link the SSH Key with Git](#2-link-the-ssh-key-with-git)
    - [3. Configure the SSH Key to solve Permission issues](#3-configure-the-ssh-key-to-solve-permission-issues)
- [Set Up Nginx](#set-up-nginx)
    - [1. Install Nginx](#1-install-nginx)
    - [2. Alter the configuration of the Webserver](#2-alter-the-configuration-of-the-webserver)
    - [3. Create the HTML file](#3-create-the-html-file)
    - [4. Restart nginx service](#4-restart-nginx-service)

## Establish a Connection to the Target Server

The first step is to establish a secure connection to the remote Linux server. SSH (Secure Shell) allows the client to remotely access and manage the server through the command line.

### 1. Generate an SSH Key

Client:

```bash
ssh-keygen -t ed25519
```

The command generates a private key and a public key.
The private key is stored locally and shouldn't never be shared. The public key can be safely copied to the server.
The generated files usually look like this, if the path and key name won't changed:

```bash 
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

During key generation, you will be prompted to enter a passphrase for the key. This serves as an additional layer of security. While entering a passphrase is optional, it is strongly recommended to protect your private key. If you choose to use one, store it securely in a password manager.

### 2. Copy the Public Key to the Server

The public key can be copied to the server using the following command:

Client:
```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub username@SERVER_IP
```

### 3. Connect Using the SSH Key

The connection can be establish with the following command:

Client:
```bash
ssh -i ~/.ssh/id_ed25519 username@SERVER_IP
```

### 4. Disable Password Authentication

> [!CAUTION]
> ⚠️ Make sure that SSH key authentication works before disabling password authentication. Otherwise, you may lose access to the server.
>

Open the config file `sshd_config` with sudo rights and edit the value `PasswordAuthentication` to `no` (The # has to be removed). 

Server:
```bash
sudo nano /etc/ssh/sshd_config
```

Restart `ssh.service` after editing and saving the config file.

Server:
```bash
sudo systemctl restart ssh.service
```

## Establish Git Access via SSH

### 1. Generate an SSH Key for Git

The SSH key can be generated the same as in the previous [step](#1-generate-an-ssh-key) and don't forget to use an other name for the key.

### 2. Link the SSH Key with Git

The content of the public key has to be copied to GitHub. 

Server:
```bash
cat ~/.ssh/<KEY_NAME>.pub
```

Go to the right top corner and click to your `Profil` and navigate to `Settings` in GitHub. Create a SSH Key under the menu `SSH and GPG Key`
enter the title and paste the key content.

### 3. Configure the SSH Key to solve Permission issues

If a permission denied error message appears after setup, the common issue is that the Server cant find the key. To solve this issue a `config` file has to be created.

Server:
```bash
touch ~/.ssh/config
```

The content of the `config` file is set as following:

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/<KEY_NAME>
    IdentitiesOnly yes
```

## Set Up Nginx

### 1. Install Nginx

Install Nginx with the following commands:

Server:
```bash
sudo apt update
sudo apt install nginx -y
```

Check thath Nginx is running on the background

Server:
```bash
systemctl status nginx.service
```

The default Website of Nginx should be seen on your browser with the IP adress of your server on the search bar

### 2. Alter the configuration of the Webserver

After installation and testing the webserver, the default configuration can be changed to alternative `index.html` instead of the nginx start page.

Create the configuration file in ``/etc/nginx/sites-enabled/` and edit it.

Server:
```bash
touch /etc/nginx/sites-enabled/alternatives
sudo nano /etc/nginx/sites-enabled/alternatives
```

Place the content below and save it.

```
server {
        listen 8081;
        listen [::]:8081;

        root /var/www/alternatives;
        index alternate-index.html;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

### 3. Create the HTML file

Ensure that the directory `/var/www/alternatives` exist. It can be checked with this command.

Server:
```bash
ls /var/www/
```

Create the directory if it doesn't exit

Server:
```bash
sudo mkdir /var/www/alternatives/
```

Create the HTML file and edit it.

Server:
```bash
sudo touch /var/www/alternatives/alternate-index.html
sudo nano /var/www/alternatives/alternate-index.html
```

For example a simple HTML code.

```html
<!doctype html>
<html>
<head>
        <meta charset="utf-8">
        <title>Hello, Nginx!</title>
</head>
<body>
        <h1>Hello, Nginx!</h1>
        <p>I have just configured our Nginx web server on ubuntu server!</p>
<body>
</html>

```

### 4. Restart nginx service

To load the new configuration the Nginx service has to be restart with the following command:

Server:
```bash
sudo service nginx restart
```

You should now see your own HTML homepage in your browser if you enter the `<Server_IP_ADRESS>:8081` in to the search bar.
