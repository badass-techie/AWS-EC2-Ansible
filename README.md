# AWS-EC2-Ansible

This project demonstrates how to provision and configure a publicly accessible AWS EC2 instance using Ansible.

## Prerequisites

- You need to have an AWS account and an IAM user with sufficient permissions to create and manage EC2 resources.

- You need to have the AWS CLI installed and configured with your AWS credentials. You can follow the instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html).

- You need to have an SSH key pair generated and uploaded to AWS. You can use the following command to generate a key pair:

  ```bash
  ssh-keygen -t rsa -b 4096 -f my_ssh_keypair_name
  ```

  Then, you can use the AWS CLI or the AWS console to upload the public key to AWS.

- You need to have Ansible installed on your machine.

    ```bash
    sudo apt update
    sudo apt install python3 python3-pip
    pip install ansible
    ```

    NOTE: Windows users can install Ansible using the Windows Subsystem for Linux (WSL).

- You need Ansible's EC2 module dependencies installed.

    ```bash
    pip install boto boto3 botocore
    ```

## Instructions

- Clone this repository or download the code as a zip file.

  ```bash
  git clone https://github.com/user/AWS-EC2-Ansible.git
  ```

- Create an ansible vault file to store your SSH private key.

  ```bash
  ansible-vault create secrets.yml
  ```

    Add the following content to the file and replace `your_ssh_private_key` with the path to your SSH private key.

    ```yaml
    ssh_private_key: your_ssh_private_key
    ```

- Visit the AWS VPC dashboard and note the VPC ID of the default VPC and the subnet ID of the default subnet. Populate the `ec2.yml` file with the VPC ID and subnet ID.

- Run the following command to create the EC2 instance:

  ```bash
   ansible-playbook --ask-vault-pass --extra-vars "@secrets.yml" ec2.yml
  ```

  You will be prompted to enter the vault password. Enter the password you used to create the `secrets.yml` file.

- To destroy the resources created by Ansible, fill in the instance ID in terminate_ec2.yml, then run

  ```bash
    ansible-playbook terminate_ec2.yml
  ```

  This will delete all the resources and free up any charges incurred by them.
