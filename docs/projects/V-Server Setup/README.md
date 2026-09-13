# V-Server Setup

This readme is a guide to configurate a v-server to be ready for ssh connection with a key pair and deactivate the user login for extra safety.

## Table of Contents

-[V-Server Setup](#V-Server-Setup)
    -[Table of Contents](#table-of-contents)
    -[Prerequisites](#prerequisites)
    -[Quickstart](#quickstart)

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition 
    link="https://github.com/Belsamor/my-dso-blog"
    title="Repository" 
    type="tip"
>
Checkout this repository to see the code/implementation
</GithubLinkAdmonition>

## Prerequisites

- Virtual-Server
- Server user with sudo permission
- Git and OpenSSH on local machine
- GitHub account

## Quickstart

1. Configure SSH access

- Connect to your server
```bash
ssh <user>@<ip-address>
```
- Add your public ssh key to the server
```bash
ssh-copy-id -i ~/.ssh/<key-name.pub> <user>@<ip-address>
```
- Use your private ssh key for server login
```bash
ssh -i ~/.ssh/<key-name> <user>@<ip-address>
```
- Check authorized_keys file for your ssh-key data
```bash
cat ~/.ssh/authorized_keys
```
- Change PW authentication config to no and remove comment
```bash
sudo nano /etc/ssh/sshd_config
```
```config
PasswordAuthentication no
```
- Restart ssh service to apply changes
```bash
sudo systemctl restart ssh.service
```
- Test if user login has been removed
```bash
ssh -o PubkeyAuthentication=no lars-hank@128.140.100.92
```

2. Install and configuration of nginx

- Update Packages
```bash
sudo apt update
```
- Install nginx
```bash
sudo apt install nginx -y
```
- Check status if nginx is working
```bash
systemctl status nginx.service
```
- Create directory
```bash
sudo mkdir /var/www/alternatives
```
- Create html file
```bash
sudo touch /var/www/alternatives/alternate-index.html
```
- Configure the alternatives file and fill it with content
```bash
sudo nano /etc/nginx/sites-enabled/alternatives
```
```nginx
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
- Open the html file and fill it with content
```bash
sudo nano /var/www/alternatives/alternate-index.html
```
- Restart nginx service for the changes to take effect
```bash
sudo service nginx restart  
```
- Restart the vm
```bash
sudo systemctl reboot
```
- Generate key on vm
```bash
ssh-keygen -t ed25519
~/.ssh/<Key name>
```
- Add key to ssh config file
```bash
nano ~/.ssh/config
```
```config
	Host github.com
	        HostName github.com
	        User git
	        IdentityFile ~/.ssh/<key name>
	        IdentitiesOnly yes

```

3. Configure Git on vm

- Clone the wanted repository
```bash
git clone git@github.com:Belsamor/my-dso-blog.git
```
- Change to repository
```bash
cd my-dso-blog
```
- Edit the .git config to set correct email and username
```bash
git config --global user.email "<email>"
git config --global user.name "<username>"
```