# V-Server Setup

This page documents how I configured my very first cloud server instance in the Developer Akademie DevSecOps Course using SSH.

## Table of Contents

<!--INSERT YOUR TABLE OF CONTENTS HERE -->

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
'''bash
ssh <user>@<ip-adress>
'''
- Add your public ssh key to the server
'''bash
ssh-copy-id -i ~/.ssh/<key-name.pub> <user>@<ip-adress>
'''
- Use your private ssh key for server login
'''bash
ssh -i ~/.ssh/<key-name> <user>@<ip-adress>
'''
- Check authorized_keys file for your ssh-key data
'''bash
cat ~/.ssh/authorized_keys
'''
- Change PW authentication config to no and remove comment
'''bash
sudo nano /etc/ssh/sshd_config
PasswordAuthentication no
'''
- Restart ssh service to apply changes
'''bash
sudo systemctl restart ssh.service
'''
2. 

## Description

this is an *example* of a **description**.

## Further References