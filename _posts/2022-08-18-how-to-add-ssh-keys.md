---
layout: post
title:  "Add ssh keys"
date:   2022-08-18 18:16:52 +0500
author: Abdul Ahad Butt
tags: ssh
desc: Use ssh-keygen to connect to your remote device without having to input your password everytime
---


# What is ssh?
ssh stands for secure socket layer. 

# Steps to copy ssh public key to remote server
1. First if you do not have a key, run the following command in a local terminal / Powershell to generate an SSH key pair:

    **macOS / Linux:** Run the following command in a **local terminal**
            
        ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519-remote-ssh

    **Windows:** Run the following command in a **local Powershell**

        ssh-keygen -t ed25519 -f "$HOME\.ssh\id_ed25519-remote-ssh"

    The -f command saves your ssh to a location


2. Authorize your Windows machine to connect
    If you're connecting to a **Linux** Host, type this command in your powershell:

    ```shell
    $USER_AT_HOST="your-user-name-on-host@hostname"
    $PUBKEYPATH="$HOME\.ssh\id_ed25519.pub

    $pubKey=(Get-Content "$PUBKEYPATH" | Out-String); ssh "$USER_AT_HOST" 
    "mkdir -p ~/.ssh && chmod 700 ~/.ssh && echo '${pubKey}' >> ~/.ssh/
    authorized_keys && chmod 600 ~/.ssh/authorized_keys"
    ```
3. Go your .ssh file location and change the SSH config file like so:

    ```yaml
    Host name-of-ssh-host-here
        User your-user-name-on-host
        HostName host-fqdn-or-ip-goes-here
        IdentityFile ~/.ssh/id_ed25519-remote-ssh
    ```