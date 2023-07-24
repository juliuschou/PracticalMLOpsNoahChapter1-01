# Upgrade Python 2.7 to 3.6 and Installing pip on CentOS 7

## Installing Development Tools

Development tools are required for building Python modules. To install the necessary tools and libraries, run the following command in the terminal:

arduinoCopy code

`sudo yum groupinstall 'Development Tools'` 

## Enable Software Collections (SCL)

Software Collections, also known as SCL, allows you to build, install, and use multiple versions of software on the same system without affecting system default packages. To enable SCL and install the CentOS SCL release file, run:

arduinoCopy code

`sudo yum install centos-release-scl` 

## Installing Python 3.6 on CentOS 7

To install Python 3.6, which is the latest version available at the time of writing, run the following command:

Copy code

`sudo yum install rh-python36` 

## Using Python 3

After installing the `rh-python36` package, you can switch to Python 3.6 by launching a new shell instance using the Software Collection `scl` tool. Execute the following command:

bashCopy code

`scl enable rh-python36 bash` 

## Install pip

To install `pip` and any required packages, run:

Copy code

`sudo yum -y install python-pip` 

## Install JetBrains Toolbox

To install JetBrains Toolbox, which is a handy tool for managing JetBrains IDEs, follow these steps:

bashCopy code

`# Download the script
curl -L -o jetbrains-toolbox.sh https://raw.githubusercontent.com/nagygergo/jetbrains-toolbox-install/master/jetbrains-toolbox.sh

# Make the script executable
chmod +x jetbrains-toolbox.sh

# Run the script
./jetbrains-toolbox.sh` 

## Create a Virtual Environment in PyCharm

To create a virtual environment in PyCharm, follow these steps:

1.  Create a new project and give it a name.
2.  Select "New environment using" and choose "Virtualenv" from the dropdown.
3.  Provide a location for the virtual environment and select the base interpreter.
4.  Optionally, check the box labeled "Inherit global site-packages" to inherit globally installed libraries.
5.  Click on the "Create" button to create the virtual environment.

To install a package to the virtual environment, you can use the command `pip install <package-name>` in the terminal or go to `File → Settings → Project → Project Interpreter` and click on the "+" icon to add a package.

## Install Required Packages

To install the required packages for your project, execute the following command:

Copy code

`pip install pytest pytest-cov coverage` 

## Implementing DevOps

1.  Create a file named `hello.py` with the following content:

pythonCopy code

`def add(x, y):
    """This is an add function"""
    return x + y

print(add(1, 1))` 

2.  Create a file named `test_hello.py` in the same folder as `hello.py` with the following content:

pythonCopy code

`from hello import add

def test_add():
    assert 2 == add(1, 1)` 

3.  Create a `requirements.txt` file with the required packages:

makefileCopy code

`coverage==6.2
pylint==2.13.9
pytest==7.0.1
pytest-cov==4.0.0` 

4.  Create a Makefile to define project tasks:

makeCopy code

`install:
	pip install --upgrade pip &&\
	pip install -r requirements.txt

lint:
	pylint --disable=R,C hello.py

test:
	python -m pytest -vv --cov=hello test_hello.py` 

## Push Code to GitHub Using SSH

Follow these steps to push code to GitHub without using a username and password:

1.  Generate an SSH Key:

mathematicaCopy code

`ssh-keygen -t ed25519 -C "your_email@example.com"` 

2.  Add the SSH Key to Your GitHub Account:
    
    -   Log in to your GitHub account.
    -   Go to "Settings" → "SSH and GPG keys."
    -   Click on "New SSH key" or "Add SSH key" and paste the contents of your public key.
3.  Install Git (if not already installed):
    

Copy code

`sudo yum install git` 

4.  Configure Git to Use SSH:

arduinoCopy code

`git config --global user.name "Your GitHub Username"
git config --global user.email "your_email@example.com"
git remote set-url origin git@github.com:YourUsername/YourRepository.git` 

5.  Create an Empty Repository on GitHub:
    
    -   Log in to your GitHub account.
    -   Click on the "+" sign and select "New repository."
    -   Give your repository a name and click "Create repository."
6.  Push Code to GitHub:
    

bashCopy code

`cd /path/to/your/project
git init
git add .
git commit -m "Your commit message here"
git push origin main` 

## Adding a Workflow to the Git Repository

To add a workflow to your Git repository using GitHub Actions, follow these steps:

1.  Create a Workflow YAML File:
    
    -   Create a new directory named `.github/workflows` in your project directory.
    -   Inside the `workflows` directory, create a YAML file (e.g., `my_workflow.yml`) that defines your workflow.
2.  Define the Workflow:
    
    -   Open the `my_workflow.yml` file and define your workflow using the YAML syntax. You can include multiple jobs and steps.
3.  Save the Workflow File:
    
    -   Save the YAML file with the defined workflow inside the `.github/workflows` directory.
4.  Commit and Push:
    
    -   Commit the workflow file to your local repository and push the changes to the remote repository.
5.  Verify the Workflow on the Remote Repository:
    
    -   Go to the "Actions" tab on your GitHub repository to see your workflow listed and running based on the specified triggers.

Now you have successfully added a workflow to your Git repository using GitHub Actions.
