
# Practical MLOps: A Step-By-Step Guide

## Introduction

Welcome to the Practical MLOps tutorial repository! This repository is a step-by-step guide to creating a new GitHub repository with the necessary Python scaffolding, employing Makefile, linting, testing, and additional steps such as code formatting as the first exercise of chapter 1 from "Practical MLOps" by Noah Gift and Alfredo Deza. Here, we also cover the details of installing and upgrading Python and other necessary development tools.

## Setup: Upgrading Python & Installing Required Tools

The first step is to ensure that you have Python 3.6 and pip installed. Follow the steps below for a CentOS 7 system:

### Installing Development Tools

1.  Open your terminal and run the following command to install necessary development tools:
        
    `sudo yum groupinstall 'Development Tools'` 
    

### Enabling Software Collections (SCL)

1.  Run this command to install the CentOS SCL release file:
    
    `sudo yum install centos-release-scl` 
    

### Installing Python 3.6

- To install Python 3.6, use the following command:
    
    `sudo yum install rh-python36` 
    

### Using Python 3.6

1.  After installing Python 3.6, check your Python version:

    `python --version` 
    
    This will likely return Python 2.7 as the default version.
2.  To switch to Python 3.6, launch a new shell instance with the SCL tool:
    
    `scl enable rh-python36 bash` 
    
3.  Check your Python version again, Python 3.6 should now be the default version.

### Installing pip

-  Finally, install python-pip and any required packages with this command:
    
    `sudo yum -y install python-pip` 
    

## Setting Up Your IDE: PyCharm & JetBrains Toolbox

Now that you have Python and pip ready, you can set up your Integrated Development Environment (IDE). Here we use PyCharm as our IDE, and JetBrains Toolbox to manage JetBrains apps.

### Installing JetBrains Toolbox & PyCharm

1.  Download the script using `curl`:
    
    
    `curl -L -o jetbrains-toolbox.sh https://raw.githubusercontent.com/nagygergo/jetbrains-toolbox-install/master/jetbrains-toolbox.sh` 
    
2.  Make the downloaded script executable:
        
    `chmod +x jetbrains-toolbox.sh` 
    
3.  Run the script:
        
    `./jetbrains-toolbox.sh`
     
4. Install PyCharm Community

### Creating a Virtual Environment in PyCharm

1.  Open PyCharm and create a new project.
2.  In the setup screen, select the option "New environment using" and choose "Virtualenv" from the dropdown.
3.  Choose a location for the virtual environment and select the base interpreter.
4.  Check the checkbox labelled "Inherit global site-packages" if you want your project’s virtual environment to inherit all globally installed libraries and packages.
5.  Click on "Create" to create the virtual environment.


## Installing Required Packages

Having set up the virtual environment, we will now install some required packages. Run the following command in your virtual environment:

`pip install pytest pytest-cov coverage` 

## Implementing DevOps

In this section, we'll develop a simple Python program and create a `Makefile` to automate some development tasks.

### Create hello.py

- In your project directory, create a new file named `hello.py` with the following content:
    ```
    def add(x, y):
        #This is an add function
        return x + y
    
    print(add(1, 1))
	 ```

### Create a Test File

-  Create a new file named `test_hello.py` in the same directory as `hello.py`. The content of the file should be:
    ```
    from hello import add
    
    def test_add():
        assert 2 == add(1, 1)` 
    ```

### Create requirements.txt

-  Create a `requirements.txt` file in the same directory. This file should include:
 
    ```
    coverage==6.2
    pylint==2.13.9
    pytest==7.0.1
    pytest-cov==4.0.0
    ```
    

### Create a Makefile

-  Create a `Makefile` in the same directory with the following recipes:

    ```
    install:
        pip install --upgrade pip &&\
            pip install -r requirements.txt
    lint:
        pylint --disable=R,C hello.py
    
    test:
        python -m pytest -vv --cov=hello test_hello.py
    ```

Now, you can use `make install`, `make lint`, and `make test` to automatically install requirements, perform linting, and run tests respectively.

## Configuring GitHub to Avoid Using Username and Password

To interact with GitHub without the need for entering a username and password every time, you can configure SSH authentication. Here are the steps:

### Generate SSH Key

- Open a terminal on your CentOS 7 machine and run the following command to generate an SSH key pair:
    
    `ssh-keygen -t ed25519 -C "your_email@example.com"` 
    

### Add SSH Key to GitHub Account

1.  Log into your GitHub account.
2.  Click on your profile picture → Settings → SSH and GPG keys → New SSH key.
3.  Paste the contents of your `id_ed25519.pub` file into the "Key" field, give your key a descriptive title, and click "Add SSH key".

### Install Git

- Install Git with the following command:
    
    `sudo yum install git` 
    

### Configure Git to Use SSH

- Set your Git username and email address, and configure Git to use SSH. Use the following commands:
    ```
    git config --global user.name "Your GitHub Username"
    git config --global user.email "your_email@example.com"
    git remote set-url origin git@github.com:YourUsername/YourRepository.git
    ```
    

## Adding a Workflow to Your Git Repository

Finally, to add a workflow to your repository, create a GitHub Actions workflow file in the `.github/workflows` directory with the name `python-app.yml`:

```
name: Python application

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.8
      uses: actions/setup-python@v2
      with:
        python-version: 3.8
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Lint with pylint
      run: |
        pip install pylint
        pylint --disable=R,C hello.py
    - name: Test with pytest
      run: |
        pip install pytest pytest-cov
        python -m pytest -vv --cov=hello test_hello.py
```
Commit and push this file to the repository, and you can observe the workflow under the "Actions" tab of your repository.

## Conclusion

This guide leads you through setting up an MLOps environment with Python on CentOS, implementing basic DevOps practices, interacting with GitHub via SSH, and adding an automated workflow to your GitHub repository. By following these steps, you will have a solid start in your MLOps journey.

I utilized ChatGPT to enhance this article, as English is my second language.
