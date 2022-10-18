In this repo I explain how to launch EC2 instance using Ubuntu AMI

Before launching EC2 you need to have VPC with Internet Gateway, Route Tables, Subnets and SG base in place

# Launching EC2
    * Open AWS EC2 console -> tab Instances
    * Click Launch Instance button
    * Select name for the instance
    * Select Ubuntu for AMI
    * Instance type use t2.micro (can be used for free tier level)
    * Create new key pair and save it
    * Edit Network settings 
    * Select your VPC, subnet and existing SG
    * Launch the instance

# Connecting to the EC2 instance using terminal
    * Firstly find your key pair filed saved previously 
    * This file needs read permission access, and to get this  you need to run this command
        chmod 400 yourKeyPair.pem
    (I used my existing bastion.pem file)
    * Connect to your instance using its Public IP
    ssh -i "bastion.pem" ubuntu@PublicIP --> public IP can be found within AWS instance details

This is the list of required tools o be installed
Docker
Git
Tree
Terraform
Kubernetes CLI
AWS CLI

# Installing required packages and tools to our EC2
    * Install tree
  sudo apt install tree -y
    - to test this I also created a few folders and files and ran command --> tree
    * Install git
  sudo apt install git -y
    To check whether git is installed  run --> git
    * Install docker
  sudo apt  install docker.io
   * Install terraform
        1.Install unzip --> sudo apt-get install unzip
        2.Confirm the latest version number on the terraform website:
            https://www.terraform.io/downloads.html
        3.Download latest version of the terraform (substituting newer version number if needed)
            wget https://releases.hashicorp.com/terraform/1.0.7/terraform_1.0.7_linux_amd64.zip
        4.Extract the downloaded file archive
            unzip terraform_1.0.7_linux_amd64.zip
        5.Move the executable into a directory searched for executables
        sudo mv terraform /usr/local/bin/
        6.Run it --> terraform --version 


# The other way(more automated) to intall all the tools is running bash script
    1. Create .sh file
   touch tools.sh
    2. Add this commands to the script and save file
#!/bin/bash
apt install docker -y
apt install netstat -y
touch file1.txt
echo "hello testing automation" >> file1.txt
rm -rf file1.txt
echo "script has completed"
    3. Run the command --> chmod +x tools.sh --> to enable executing file permissions
    4. Run the command --> sudo ./tools.sh --> to execute the file
    5. test it  --> service nginx status