Please use amazon Linux 2 OS. 

# Installation Steps

### Install Development Tools and Dependencies

Installs essential development tools and libraries needed for compiling and building software.

```bash
sudo yum groupinstall -y "Development Tools"
```

Installs development headers and libraries for OpenSSL, bzip2, and libffi, required for Python.


```bash
sudo yum install -y openssl-devel bzip2-devel libffi-devel
```


### Install Python 2.7.18

Downloads Python 2.7.18, extracts it, configures the build with optimizations enabled, and installs it without replacing the system-provided Python.


```bash
cd /usr/src
sudo wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tgz
sudo tar xzf Python-2.7.18.tgz
cd Python-2.7.18
sudo ./configure --enable-optimizations
sudo make altinstall
```

Verifies the installed Python version.


```bash
python2.7 -V
```

### Install pip for Python 2.7

Downloads and installs pip for Python 2.7.


```bash
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python get-pip.py
```

### Install Python Packages

Installs Flask, Boto (for AWS SDK), and configparser Python packages using pip.


```bash
pip install Flask
pip install boto
pip install configparser
```

### Install Git

Installs Git, a version control system.

```bash
yum install git -y
```

### Clone the TicTacToe Project Repository

Clones the TicTacToe project repository from GitHub into the `/home/ec2-user/` directory.

```bash
cd /home/ec2-user/
git clone https://github.com/avizway1/tictactoe-with-DynamoDB.git
```

Create a file inside the code location provide file name as "config.ini" and add below entry. make sure to change the region accordingly.

[Settings]
TableName = Games
Region = ap-south-2


Also, edit the config file and edit the endpoint to "dynamodb.ap-south-2.amazonaws.com"

Also, Dont forget to attach an IAM role, that has valid access to create a DynamoDB table.

```
