## Ansible Configuration Management
Integrating  Jenkins Pipeline With Github Webhook on Jenkins-Ansible EC2 Instance to install Wireshark on webservers,db, nfs server and lb server


## Prerequisites
- Linux
- AWS 
- Jenkins Server- To act as Bastion server
- Github- Create a Repository for the Project


## Step 1. Installing Ansible on Jenkins Server
Navigate to AWS Dashboard and start jenkins server, ssh into it using public ip and install ansible using command
![Images](Jenkins-Ansible.png)

ssh into jenkins-ansible server
```sh
   ssh -i "ubuntu_lb.pem" ubuntu@public ip
```
![Images](ssh-into%20ec2%20instance.png)

Install ansible
```sh
   sudo apt update
   sudo apt install ansible
```
![Images](Installing-ansible.png)

## Step 2. Creating a Repo on Github account
Navigate to Github account and create a new repository called "ansible-config-mgt"
![Images](ansibel-config-mgt-repo.png)

Creating Webhook on the Github Repo using Jenkins environment Url
![Images](github-webhook.png)

Veryfying the Webhook has been configured
![Images](webhook-configured.png)

## Step 3. Configure Jenkins Job to Build 
Navigate to Jenkins on browser using the Public Ip and port and login to create a job
![Images](freestyle-Project.png)

Create the job with Source code Management, Build ,Triggers and Post-Build to Archive 
![Images](ansible-job.png)

![Images](Triggers.png)

![Images](post-build.png)

## Step 4. Clonnning the Repository
Navigate to github and copy the url to the repo
ssh into the jenkins server to clone
![Images](cloning%20github%20repo.png)

Update Readme with content and push code
![Images](pushing%20to%20Github.png)

Confirmig the Build on Jenkins 
![Images](Jenkins%20Build.png)

Checking the file is being archived in the path
```sh
  
```
![Images](build%20archive.png)

## Create  a new Branch
On the Jenkins server inside the repo a new branch is created.
![Images](new%20branch.png)

On the Local machine after cloning the repo a new branch is created to create the ansible files
![Images](New%20feature%20Branch.png)

## Setting up ssh Agent to connect Vscode with Jenkins-Ansible Instance
on the directory where the ssh key is mine is in the downloads folder
```sh
   cd \Downloads
   eval `ssh-agent`
```
![Images](Vscode%20ssh%20to%20Jenkins-server.png)

Update the inventory files
![Images](inventory%20updated.png)

Create and update Playbook folder
![Images](update%20common-yml%20file.png)

Pushing the code to Github
from the local machine the code is pushed to github on the feature branch to create a pull request
![Images](git%20commit.png)

Create a Pull Request from Github Repo
![Images](merge%20request.png)

Merging a Pull Request after checking everything is ok
![Images](merge%20pull%20request.png)

## Create a Pull Request from the Jenkins Server on the main branch
ssh into  jenkins-Ansible server using the agent from Vscode
then create a pull in the cloned repo
```sh
    cd ansible-config-mgt
    git pull
```
![Images](pull%20from%20jenkins%20server.png)
## Running the Playbook
Ensure all the instance are up and running
![Images](runnning%20instances.png)

![Images](Running%20Playbook.png)

Veryfying the wireshark has been installed
![Images](confirming%20Wireshark%20installed.png)

Project Completed Next is Ansible Refactoring...
Ansible is Very Interesting tool for DevOps