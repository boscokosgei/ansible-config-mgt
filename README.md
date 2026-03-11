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
Ansible is Very Interesting tool for DevOps..

## Jenkins Job Enhancement
Creating an ansible directory to store artifacts
![Images](Ansible-new%20Directory.png)

Create a new project to save artifacts into the created directory after ansible job build
![Images](arifacts-plugin.png)

After installing plugin Create a job
![Images](save_artifacts%20job.png)

Update configurations on job
![Images](Configure-Updated.png)
![Images](Build-Steps.png)

Confirming after successful Build
![Images](Artifacts%20Tested%20after%20push.png)
![Images](save-Artifacts%20Build%20Successful.png)

## Refactoring Ansible Playbook by importing other playbooks
Starting on a new branch to create features
a new branch called refactor is created 
![Images](refactor%20Branch.png)

Importing common.yml file to playbook
![Images](imporing%20Playbook%20common.yml.png)

Create a new Playbook common-del.yml to test after importing
![Images](update%20common-del-yml%20file.png)

Pushing the code to Github
![Images](Pushing%20refactored%20code.png)

Create a Pull request
![Images](Pull%20request%20on%20refactor%20Branch.png)

Merging the branch to main after reviewing the code and resolving any conflicts
![Images](changes%20merged.png)

Runnning the Playbook
![Images](Running%20Playbook.png)

Veryfying the Playbook was successfully by checking wireshark if it has been deleted
![Images](wireshark%20deleted.png)

## Creating New UAT webservers with a role webserver
Launch new EC2 Instance Running RHEL 9 Images on the two webserver.
Create 2 webserver Web1-UAT and Web2-UAT
![Image](Web1-UAT.png) ![Images](Web2UAT.png)

Running the Instances
![Images](web-servers-UAT%20Launched.png)

create roles folder
![Images](Roles%20folder.png)

The roles structure folder
![Images](roles%20folder.png)

Updating the uat.yml files with the IP addresses of the new Server
![Images](uat_yml.png)

Update task folder in webserver with main.yml
![Images](tasks.yml.png)

in the static folder creating a file to reference the roles
![Images](webservers.png)

Pushing the Changes to Github
![Images](Git%20Push%20file.png)

Create a Pull Request
![Images](PR-Request.png)

Merging the code aftere review and resolving the conflicts
![Images](Merged%20Code.png)

Runnning the Playbook
![Images](Playbook%20with%20error.png)
![Images](Ansible_playbook%20running.png)
![Images](playbook%20on%20uat-servers.png)

Checking for apache if its installed in one of uat servers
![Images](apache%20running.png)

Updating Security Group on Port 80 for the website to be accessible
![Images](SG%20http.png)

Accessing the website using public ip of Uat webserver1
![Images](Uat-web1%20Server%20Accessible.png)
