In this project we are working to develop a simple Tic-Tac-Toe game application using AWS services. The main components of this project include:

1. **AWS EC2 Instance**: This is where the application will run. We're using an Amazon Linux 2 EC2 instance to host the application.
2. **AWS DynamoDB**: This is used as the backend database to store game state and user data. DynamoDB is a NoSQL database service provided by AWS, which is fully managed and designed for high-performance applications.
3. **Python Application**: The application is written in Python, using Flask for the web framework and Boto for interacting with DynamoDB.
4. **IAM Role**: IAM role for secure connection between ec2 to dynamoDB.

### Project Structure and Components

1. **EC2 Instance Setup**:
   - **Amazon Linux 2**: An Amazon Linux 2 EC2 instance is set up to host the application.
   - **Application Deployment**: The Tic-Tac-Toe application is deployed on this instance.

2. **DynamoDB for Backend Storage**:
   - **Games Table**: A DynamoDB table named `Games` is created to store the state of each game, including information about the players, game status, and board state.
   - **Connection Manager**: A `ConnectionManager` class is used to manage connections to DynamoDB, including setting up the connection and handling queries and updates to the table.

3. **Python Application Components**:
   - **Flask Framework**: Used to handle web requests and render the game interface.
   - **GameController Class**: Manages the game logic, including creating new games, accepting or rejecting game invites, updating the game board, and determining the game result.

### Key Features and Workflow

1. **Create New Game**:
   - A new game can be created by specifying the game ID, creator, and invitee.
   - The game state is initialized and stored in the DynamoDB `Games` table.

2. **Accept/Reject Game Invite**:
   - Players can accept or reject game invites. The game status is updated accordingly in DynamoDB.

3. **Update Game Board**:
   - Players take turns to make moves by updating the board state. Each move is validated and recorded in DynamoDB.
   - The `updateBoardAndTurn` method is used to update the board and switch turns between players.

4. **Check Game Result**:
   - After each move, the game state is checked to determine if there's a win, loss, tie, or if the game is still in progress.
   - The `checkForGameResult` method checks various win conditions and updates the game status in DynamoDB accordingly.

5. **Game State Management**:
   - The game state, including player moves and game status, is stored and managed in DynamoDB.
   - The `GameController` class handles all interactions with DynamoDB to ensure the game state is consistently updated and retrieved.


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

Also, edit the config file and edit the config file and set region and endpoint based on your resources. Example mentioned below

[dynamodb]
region=ap-south-2
endpoint=dynamodb.ap-south-2.amazonaws.com

Also, Dont forget to attach an IAM role, that has valid access to create a DynamoDB table. Also, While launching EC2 instance, Enable "metadata" to "V1 and v2" instead of only V2, as we are using metadata URL to obtain the temp credentials.

Once all content is ready, Navigate to the project location and run below command. 
#make sure to open required port (5000) in ec2 security group

```bash
python application.py --config config.ini --mode service --endpoint dynamodb.ap-south-2.amazonaws.com --serverPort 5000
```

Then Open browser and enter **http://instance-public-ip:5000/** and enter to access the application.
