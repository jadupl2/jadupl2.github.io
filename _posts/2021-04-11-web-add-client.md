---
title:          How-to add a SADMIN client
desc:           How-to add a client via the web interface & setup ssh keys
version:        2.1
updated:        2021-05-13
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ how-to ] 
categories:     [ how-to ] 
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---

{% include sadm/sadm_page_info.md %}


### Steps to Add a system
- Add the server with the web interface  
- Add the SADMIN root user public key to the new client  

Each of these steps are described below.  


### Add the server with the web interface  

To add a server to SADMIN inventory, click on "Server" in the "CRUD Operations" 
([C]reate [R]ead [U]pdate [D]elete) section at the bottom left of the page.



    You will be directed to a page that list all your actual SADMIN clients.
    With this view you can "Update", "Delete" or "Create" servers.
    To add a new server into SADMIN inventory, simply press the "Create" button at the top right of the page.



    The page below will then appear and you need to enter the information concerning your server.
    You can come back later in "Update" mode to modify any of these information.
    When all the information is entered, just press the "Create" button at the button of the screen.




Add the SADMIN 'root' user public key to the new client

    Every day your new SADMIN client will produce performance data (via nmon), information that may be used for disaster recovery situation, monitoring reports, start scheduled O/S update, scripts results (log and rch files) that will inform you about the status of your systems.
    To accomplish this, the SADMIN server need to have root access to client via ssh.
    To automate the ssh access and to do it in a safely and secure manner we will use the ‘public-key authentication’.
    So this automated access will be only be possible from the SADMIN server to the clients.
    Any systems or users that tries to SSH to your SADMIN clients using the ‘root’ user, will get the ‘Permission denied’ message.
    In this example, the SADMIN server hostname is ‘holmes.maison.ca’ and the SADMIN client is "raspi7.maison.ca”.
    We will now automate the ssh login from ‘holmes.maison.ca’ to ‘raspi7.maison.ca’.

    Trying ssh to client before changing anything
        Before we change anything, let’s try to ssh to ‘raspi7’.
        Since this is the first time we are trying to access 'raspi7' from ‘holmes.maison.ca’, it ask us a confirmation.
        After answering ‘yes’, ‘raspi7’ server key is added to the user (root) known hosts file (/root/.ssh/known_hosts) on the SADMIN server.

    As you can see, we can’t logon to the client using the ‘root’ user.

    root@holmes~# ssh root@raspi7
    The authenticity of host 'raspi7 (192.168.1.25)' can't be established.
    ECDSA key fingerprint is SHA256:v1d0mK15pA9NtrhqbzFIu4boQoot99UxCi+aFcMs394.
    ECDSA key fingerprint is MD5:99:4e:d6:3a:65:e1:bb:40:ec:ce:da:3b:52:63:ee:f1.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'raspi7,192.168.1.25' (ECDSA) to the list of known hosts.
    root@raspi7's password:
    Permission denied, please try again.
    root@raspi7's password:
    Permission denied, please try again.
    root@raspi7's password:
    Permission denied (publickey,password).
    root@holmes~#



    Does user 'root' already have a public and private key ?
        On the SADMIN server ('holmes'), verify in the ‘root’ user HOME directory (/root), it should have a directory called ‘.ssh’.
        The '.ssh' directory should contains a private key (id_rsa) and a public key (id_rsa.pub).

        Your /root/.ssh directory should look a bit like this.


        root@holmes~# ls -l /root/.ssh
        total 48
        -rw-r-----  1 root root  1187 Oct  3  2017 authorized_keys
        -rw-------  1 root root  1675 Feb 23  2016 id_rsa
        -rw-r--r--  1 root root   403 Feb 23  2016 id_rsa.pub
        -rw-r-----  1 root root 26291 Jul 17 09:27 known_hosts
        root@holmes~#


    You don't have ‘root’ private and public key (id_rsa and id_rsa.pub), run command below:
        If you have these files (id_rsa and id_rsa.pub) then skip this step.
        If you don’t, run the command below to generate the 'root' user private and public key.
        When ask for a passphrase just press [ENTER] to have a blank password.


        root@holmes~/.ssh# ssh-keygen -b 4096 -C "SADMIN server"
        Generating public/private rsa key pair.
        Enter file in which to save the key (/root/.ssh/id_rsa):
        Enter passphrase (empty for no passphrase): [press ENTER]
        Enter same passphrase again: [press ENTER]
        Your identification has been saved in /root/.ssh/id_rsa.
        Your public key has been saved in /root/.ssh/id_rsa.pub.
        The key fingerprint is:
        SHA256:3dd5vZTTv3i8Qa0osnOmp5d0wVKh3Dl2ZziNpvwp3To SADMIN server
        The key's randomart image is:
        +---[RSA 2048]----+
        |           ..    |
        |         . o.. + |
        |          oo= * +|
        |         ..+o= =*|
        |        S ..+..**|
        |          . .=o+=|
        |        ...oo *oo|
        |        .o*. .E+o|
        |        +O   .o+.|
        +----[SHA256]-----+
         
        root@holmes~/.ssh# ls -l id*
        -rw------- 1 root root 1675 Jul 17 09:53 id_rsa
        -rw-r--r-- 1 root root  395 Jul 17 09:53 id_rsa.pub


    Copy the SADMIN server public key to clipboard client:
        First on the SADMIN server do ;
            Do a md5sum of the public key (Get a checksum of the file).
            Do a 'ls' command of the public key (get size of the file).
            Show the file content and copy the content to the clipboard


        root@holmes~/.ssh # md5sum id_rsa.pub
        9267667a0f04d523c7917885a4783b23  id_rsa.pub

        root@holmes~/.ssh # ls -l id_rsa.pub
        -rw-r--r-- 1 root root 403 Feb 23  2016 id_rsa.pub

        root@holmes~/.ssh # cat id_rsa.pub
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/bD8HxYuE/uZfG5ih+xLclsSMg0E6hT3aE1W6ZpMdz5w0Fr2/k9z+QdWkrD
        8xWphP3wjdWjmZg37vLcYDzHN3F3SeBUVF2CFi0/P0gDP8wFOvWCSQMuv4ifZfSYCx+kypySDOe6xoEvRmDz4o1MA3hu56R2m8
        ZP7su1yFem3P6s1cG/QveUafUpTpnyubwsEoUrS9SVt18jLWfNCTgt2yICu8dJmIpNq7Yzxx8FxT+eW6ujWAhVCZ7+Clo71tdw
        a83tCvpNrGMK6+lx4dfXjLQdD5z4+bq30CVJHQT8gaenoIzaRQ58bnDxhN4IHVOmDa7H2qLRQ1tdXqk1qCsq5t root@holmes.maison.ca


    Paste the SADMIN server public key into sadmin.pub file on the client:
        Open your favorite editor and paste the content of the public key of 'holmes' to that new file (sadmin.pub).
        Remember, you MUST not add anything to this file (no newline or carriage return), it must be identical to the one on 'holmes'.
        Save the file and verify the size and the checksum MUST be identical has the one you had on 'holmes'.
        If they are not identical the 'ssh' connection won' t work.


        root@raspi7~/.ssh# vi sadmin.pub
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/bD8HxYuE/uZfG5ih+xLclsSMg0E6hT3aE1W6ZpMdz5w0
        Fr2/k9z+QdWkrA8xWphP3wjdWjmZg37vLcYDzHN3F3SeBUVF2CFi0/P0gDP8wFOvWCSQMuv4ifZfSYCx+kyp
        ySDOe6xoEvRmDz4o1MA3hu56R2m7ZP7su1yFem3P6s1cG/QveUafUpTpnyubwsEoUrS9SVt18jLWfNCTgt2y
        ICu8dJmIpNq7Yzxx8FxT+eW6ujWAhVCZ7+Clo71tdao83tCvpNrGMK6+lx4dfXjLQdD5z4+bq30CVJHQT8ga
        enoIzaRQ58bnDxhN4IHVOmDa7H2qLRQ1tdXqk1qCsq5t root@holmes.maison.ca
        ~                                                                                   
        ~                                                                                   
        ~                                                                                   
        ~                                                                                   
        ~                                                                                   
        "sadmin.pub" [New File]

        root@raspi7~/.ssh# ls -l sadmin.pub 
        -rw-rw-r-- 1 root root 403 Oct  7 13:13 sadmin.pub

        root@raspi7~/.ssh# md5sum sadmin.pub 
        9267667a0f04d523c7917885a4783b23  sadmin.pub


    Include SADMIN server public key into the 'authorized_keys' file
        The last thing to do is to add our public key at the end of the 'authorized_keys' file.
        Note, that the 'authorized_keys' file may not exist, before typing the command below.


        root@raspi7~/.ssh# cat sadmin.pub >>authorized_keys


    Testing our connection to the new client
        Run the two commands below to confirm that our automated connection to 'raspi7' work as expected.
        As you can see, we where able to display the system date on 'raspi7' without having to enter a password (Success!).
        Important: We need to test with and without the domain name


        root@holmes:~# ssh raspi7 date
        Fri Aug 31 10:48:36 EDT 2018

        root@holmes:~# ssh raspi7.maison.ca date
        Fri Aug 31 10:48:39 EDT 2018


    Our client is now configure to work with SADMIN.



