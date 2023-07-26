
# Practical MLOps: A Step-By-Step Guide

Create a new GitHub repository with necessary Python scaffolding using a Makefile, linting, and testing. Then, perform additional steps such as code formatting in your Makefile.


## Introduction

Welcome to the Practical MLOps tutorial repository! This repository is a step-by-step guide to creating a new GitHub repository with the necessary Python scaffolding, employing Makefile, linting, testing, and additional steps such as code formatting as the first exercise of chapter 1 from "Practical MLOps" by Noah Gift and Alfredo Deza. Here, we also cover the details of installing and upgrading Python and other necessary development tools.

## Setup: Upgrading Python & Installing Required Tools

The first step is to ensure that you have Python 3.6 and pip installed. Follow the steps below for a CentOS 7 system:

### Installing Development Tools

1.  Open your terminal and run the following command to install necessary development tools:
        
    `sudo yum groupinstall 'Development Tools'` 
    

### Enabling Software Collections (SCL)

-  Run this command to install the CentOS SCL release file:
    
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

![image](https://github.com/juliuschou/PracticalMLOpsNoahChapter1-01/assets/4725611/44304074-2ae9-4078-9b6e-837984bda4ce)

Source: Practical MLOps by Noah Gift, Alfredo Deza

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
## Create an Empty Repository on GitHub    
Before you can push your code, you need to create an empty repository on GitHub:
1. Log in to your GitHub account.
2. Click on the "+" sign in the top right corner of the GitHub website.
3. Select "New repository" from the dropdown menu.
4. Give your repository a name and, optionally, a description.
5. Choose if you want your repository to be public or private (private repositories may require a paid GitHub plan).
6. Do not select any checkboxes for initializing the repository with README, .gitignore, or a license, as we'll push an existing repository.
7. Click on the "Create repository" button.

## Push Code to GitHub
Now that you have generated an SSH key, added it to your GitHub account, configured Git to use SSH, and created an empty repository on GitHub, you can push your code to GitHub:
```
# Navigate to your project directory (the directory where your code is located) 
cd /path/to/your/project # Initialize Git (if not already initialized) 
git init 
# Add the files you want to commit to the staging area 
git add . 
# Commit the changes with a meaningful message 
git commit -m "Your commit message here" 
# Push the committed changes to the master branch of your GitHub repository 
git push origin master
```


## Adding a Workflow to Your Git Repository


Finally, to add a workflow to your repository, create a GitHub Actions workflow file in the `.github/workflows` directory with the name `python-app.yml`:

Here are the steps to add a workflow to your Git repository:

1. Create a Workflow YAML File:

- In your local project directory, create a new directory named .github/workflows. This is where GitHub Actions will look for workflow files. Inside the workflows directory, create a YAML file with a meaningful name, for example, my_workflow.yml. This file will define the steps and jobs for your workflow.

2. Define the Workflow: 

- Open the my_workflow.yml file in a text editor and define your workflow using the YAML syntax. The workflow can have one or more jobs, and each job can consist of multiple steps. Here's a simple example of a workflow that runs on every push to the main branch:

- This example workflow consists of a single job named "build." It runs on every push event to the "main" branch, and it includes two steps: one to check out the repository code and another to build the project.


```
name: Azure Python 3.5
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.7.17
      uses: actions/setup-python@v1
      with:
        python-version: 3.7.17
    - name: Install dependencies
      run: |
        make install
    - name: Lint
      run: |
        make lint
    - name: Test
      run: |
        make test 
```
3. Commit and Push:

- After creating and saving the workflow file, you need to commit it to your local repository and push the changes to the remote repository. Use the following commands:

```
git add .github/workflows/my_workflow.yml
git commit -m "Add my_workflow.yml"
git push origin main
```
4. Verify the Workflow on the Remote Repository:
- Once the changes are pushed to the remote repository, navigate to the repository on GitHub or your Git hosting platform. Go to the "Actions" tab, and you should see your workflow listed there. GitHub Actions will automatically detect the new workflow file and start running it based on the defined triggers.
  
## Conclusion

This guide leads you through setting up an MLOps environment with Python on CentOS, implementing basic DevOps practices, interacting with GitHub via SSH, and adding an automated workflow to your GitHub repository. By following these steps, you will have a solid start in your MLOps journey.

I utilized ChatGPT to enhance this article, as English is my second language.
