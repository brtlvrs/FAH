# Brtlvrs Folding @ Home Ansible project

|version| 0.3 | [MIT license](LICENSE)|Copyright (c) 2020 Bart Lievers|[blog](https://vblog.bartlievers.nl)|
|---|---|---|---|---|

This repository contains my approach for building, maintaining an running a Folding @ Home docker container.

## Folding @ Home initiative

For information about Folding @ Home, please check their website at [foldingathome.org](https://foldingathome.org)

## Goal

To get some experience with Ansible, git, docker while helping a great intiative.

## History

|version|History|
|---|---|
|v0.3|moved from centOS to debian for smaller image (from 488 MB to 83 MB)
|v0.2|centOS version with restructured Ansible rule
|v0.1|no idea :-)

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
You can enter your F@H details (username,team id, passkey) in ansible defaults file at [roles/FAH/defaults/main.yaml](roles/FAH/defaults/main.yaml)

```bash
ansible-playbook playbook-FAH.yaml --tags run
```

This will create the docker image and starts a container of it.
The image is based on centos v 7.7.1908
dockerfile and config.xml (for the FAHClient) are dynamicly templated by ansible during the build process of the image.

To only run the image

```bash
ansible-playbook playbook-FAH.yaml --tags run_only
```

## build and archive

It is also possible to only build, or build and archive the docker image.
Archiving is usefull when you want to use the same image on other docker instances.
I have it also running on a Synology DSM.

To only build the image.
The container will be stopped and removed before the image is rebuild.

```bash
ansible-playbook playbook-FAH.yaml --tags build
```

To only archive the image.

```bash
ansible-playbook playbook-FAH.yaml --tags archive_only
```

Importing an running the archived image on another docker instance

```bash
docker load < (name of archive).tar
docker run -d --name FAH -p 7396:7396/tcp -p 36330:36330/tcp (name of imported docker image)
```

## tags

Tags are used to run a selection of the tasks.
Run below code, to display the functions of the tags

```bash
ansible-playbook playbook-FAH.yaml --tags help
```

|tag|stop<br>container|remove<br>container|remove<br>container&<br>volume|remove<br>image|build<br>image|run<br>container|Archive<br>image|Remove<br>build<br>folder|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||
|run<br>(default)||x||x|x|x||x
|run_only||||||x||x
|clean_run|x||x|x|x|x||x
|stop|x|||||||x
||
|build|x|x||x|x|||x
|build_only||||x|x|||x
||
|archive||x||x|x||x|x

## Todo

- more documentation
- testing other container OSes
  - photonOS
  - Alpine
