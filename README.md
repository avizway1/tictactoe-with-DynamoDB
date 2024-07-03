# Python 2.7 and Dependencies Installation Guide

This guide provides step-by-step instructions for installing Python 2.7 and its dependencies on a Linux system, specifically for CentOS/RHEL-based distributions using yum package manager.

## Installation Steps

```bash
# 1. Install Development Tools and Dependencies
sudo yum groupinstall -y "Development Tools"
sudo yum install -y openssl-devel bzip2-devel libffi-devel

# 2. Download and Extract Python 2.7.18
cd /usr/src
sudo wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tgz
sudo tar xzf Python-2.7.18.tgz

# 3. Configure and Install Python 2.7.18
cd Python-2.7.18
sudo ./configure --enable-optimizations
sudo make altinstall

# 4. Verify Python Installation
python2.7 -V

# 5. Install pip (Python Package Installer)
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python get-pip.py

# 6. Install Required Python Packages
pip install Flask
pip install boto
pip install configparser

# 7. Install Git
yum install git -y

# 8. Clone a GitHub Repository
cd /home/ec2-user/
git clone https://github.com/avizway1/tictactoe-with-DynamoDB.git