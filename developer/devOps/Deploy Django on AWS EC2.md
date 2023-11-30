We will learn how to deploy Django project on AWS EC2 instance

1. Create EC2 instance on AWS console
2. Configure a security group

- HTTP (80)
- HTTPS (443)
- TCP (8000)

1. Connect to EC2 instance using puTTY or WinSCP or SSH

> NOTE: Download PEM file, the username is `ubuntu` when trying to connect

1. Install nginx, python, vim

```bash
sudo apt-get update
sudo apt-get install nginx
sudo apt-get install vim
sudo apt-get install python3-dev python3-venv python3-pip
```

1. Create user for django app

```bash
sudo useradd -b /home -m -s /bin/bash django
sudo usermod -a -G www-data django
sudo suermod -a -G www-data ubuntu
```
