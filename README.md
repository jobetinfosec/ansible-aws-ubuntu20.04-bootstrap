# Initial setup of Ubuntu 20.04 server on Amazon AWS Cloud Platform


## Description

Initial setup of Ubuntu 20.04 server on Amazon AWS Cloud Platform

## Tasks

* System update
* Check if reboot is required
* Set no password in sudoers file
* Set timezone
* Install glances and net-tools
* SSH hardening
* Add aliases to .bashrc file

## Tested on

Ubuntu 20.04 server


## Prerequisites

a) Amazon AWS account<br />
b) Amazon AWS CLI tool already installed in your laptop and setup with your AWS account credentials<br />
c) An Amazon AWS SSH key pair (.pem) on your laptop, with the public key already installed in the remote server<br />
d) An Amazon EC2 instance (Virtual machine) with Ubuntu 20.04 already installed<br />



## Instructions

a) On your laptop create a working directory


b) In your working directory open a console window


c) Clone github repository

```
git clone https://github.com/jobetinfosec/ansible-aws-ubuntu2004-bootstrap.git
```


d) Switch to playbook directory

```
cd ansible-aws-ubuntu2004-bootstrap
```


e) Open the hosts file

```
nano hosts
```

f) Replace <TEMPORARY_ITEMS> with your own data:

| Item | Instructions | Further info |
| --- | --- | --- |
| `<SERVER_IP>` | replace <SERVER_IP> with your server's IP address |  |
| `<SSH_KEY_NAME>` | replace it with your SSH key name | For example: ~/.ssh/key_name.pem |


then save and close the file


g) Open the roles/sudo/defaults/main.yml file

```
nano roles/sudo/defaults/main.yml
```

h) Replace <TEMPORARY_ITEMS> with your own data:

| Item | Instructions | Further info |
| --- | --- | --- |
| `<PASSWORD_HASH>` | replace <PASSWORD_HASH> with the hash of sudo user's password | to create a password hash use mkpasswd --method=sha-512 command. If mkpasswd is not installed, install it with apt-get install whois |
| `SSH_KEY_NAME` | replace it with your SSH key name | For example: ~/.ssh/key_name.pem |

then save and close the file


i) Open the roles/bootstrap/defaults/main.yml file

```
nano roles/bootstrap/defaults/main.yml
```

j) Replace <TEMPORARY_ITEMS> with your own data:

| Item | Instructions | Further info |
| --- | --- | --- |
| `<CUSTOM_SSH_PORT>` | replace <CUSTOM_SSH_PORT> with the custom SSH port number you wish to setup |  |
| `TIMEZONE` | replace it with your current timezone | For example: Europe/Rome |

then save and close the file


k) Check if you are able to ping remote server

```
ansible -m ping all
```

You should receive a SUCCESS message


l) Check if any error shows up

```
ansible-playbook bootstrap.yml --check
```


m) Launch installation

```
ansible-playbook bootstrap.yml
```


## Licence

MIT licence

## Author Information

Created by Roberto Jobet (sysadmin@wpsecurity.press).

Don't hesitate to open an Issue if you find any bug or have suggestions.
