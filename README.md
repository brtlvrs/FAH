# Brtlvrs Folding @ Home Ansible project

|version| 0.2 | MIT license|Copyright (c) 2020 Bart Lievers|[blog](https://vblog.bartlievers.nl)|
|---|---|---|---|---|

This repository contains my approach for building, maintaining an running a Folding @ Home docker container.

## Folding @ Home initiative

For information about Folding @ Home, please check their website at [foldingathome.org](https://foldingathome.org)

## Goal

To get some experience with Ansible, git, docker while helping a great intiative.

## My environment

My docker containers run on VMware photon OS.
And I've installed Ansible for my configuration management of the host and docker containers.

Details:
||||
|---|---|---|
|VM|||
||Virtualization| vmware|
||Operating System| VMware Photon OS/Linux| 
||Kernel| Linux 4.19.104-1.ph3-esx|
||Architecture|x86-64|
|Ansible| | |
||version|2.8.3|
||python|2.7.17|
|Docker|||
|| Engine| Community |
||version|18.09.9|

## Run

The playbook will create a docker container from scratch and run it.
You can enter your F@H details (username,team id, passkey) in ansible defaults file at roles/FAH/defaults/main.yaml

```bash
ansible-playbook playbook-FAH.yaml --tags run
```

This will create the docker image and starts a container of it.
The image is based on centos v 7.7.1908
dockerfile and config.xml (for the FAHClient) are dynamicly templated by ansible during the build process of the image.

## build and archive

It is also possible to only build, or build and archive the docker image.
Archiving is usefull when you want to use the same image on other docker instances.
I have it also running on a Synology DSM.

To only build the image

```bash
ansible-playbook playbook-FAH.yaml --tags build
```

To only archive the image

```bash
ansible-playbook playbook-FAH.yaml --tags archive
```

Importing an running the archived image on another docker instance

```bash
docker load < (name of archive).tar
docker run -d --name FAH -p 7396:7396/tcp -p 36330:36330/tcp (name of imported docker image)
```

## Todo

- more documentation
- testing other container OSes