# Brtlvrs Folding @ Home Ansible project

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
