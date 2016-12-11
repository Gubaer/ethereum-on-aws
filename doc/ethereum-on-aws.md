# Ethereum on Amazon EC2

## Prepare Amazon AWS

### Create an Amazon AWS login
If you don't have an Amazon AWS account yet, [create one][1].

### Create an Amazon user

1. lauch the AWS management console
2. select the service **IAM**
3. show the list of users
4. click on **Add User** and create a new user, i.e. the user `ethereum`

Give the new user full permissions to access EC2.

5. click on the new user
6. select the tab **Permissions**
7. click on **Add Permissions**
8. select **Attach existing policies directly**
9. select the policy **AmazonEC2FullAccess**

Create a new access key for the user

10. selec tab **Security Credentials**
11. click on **Create Access Key** 
12. write down the created **access key ID** and the **secret access key**. You'll need both parameters later. 

### Create a new key pair
Later you will need a key pair (consisting of a private a public key) in order
to access the EC2 instances via `ssh`. You have to download the private key of this key pair and copy it to you management node.

1. launch the AWS management console
2. select the service **EC2**
3. select **Key Pairs** in the menu on the left
4. click on **Create Key Pair**
5. select a name, i.e. ``ethereum``
6. save the generated private key `<your-key-pair-name>.pem` 

## Prepare the managemenet node

The following instructions assume that you have a node running Ubuntu 16.04. This could be 
* a physical machine 
* a virtual machine, in my case for instance a VirtualBox VM running Ubuntu 16.04 on Windows 10 as host operating system
* an EC2 instance which you setup and configure as management node 

### Install Ansible
You have to install `ansible` according to the ansible [documentation](http://docs.ansible.com/ansible/intro_installation.html).

In short, on Ubuntu run the following commands
```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

### Add .boto configuration file
Under the hood `Ansible` uses the python package `boto` to connect to the AWS management API.  

Add the following configuration entries to the `$HOME/.boto` configuration file (create it, if it doesn't exist yet).

```INI
[Credentials]
aws_access_key_id#<the key>
aws_secret_access_key#<the secret>

[Boto]
ec2_region_name#eu-west-1
```

### Retrieve Ansible playbooks from the git repository


### Configure the Ansible playbooks


## Provision Ethereum network on Amazon EC2

```shell
% ansible-playbook provision.yml
```


## Stop Ethereum network on Amazon EC2


## Start Ethereum network on Amazon EC2


## Terminate Ethereum network on Amazon EC2
This will terminate all the EC2 instances and delete the attached block storage volumes.

**Warning: this playbook entirely deletes the  private ethereum blockchain which is managed on these nodes!**

```shell
% ansible-playbook terminate.yml
```



[1]: https://portal.aws.amazon.com/billing/signup?redirect_url#https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/support



