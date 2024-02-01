# Project 1: Solitude [Derived Project: Olympus]

The goal of this project is to create an EC2 instance and an S3 Bucket to be able to transfer 100 files from the EC2 to the S3 Bucket.  
However, there is a big twist. Anything that is required to be done on the EC2 cannot be done manually. There will be additional requirements to ensure this happens.  
Lastly, All the resources must be done in pipelines.

## Primary Goal:

This is the cloudformation goals set from Olympus:
  * Security Group CFT created with open outbound and inbound access.
  * IAM Role CFT created
  * KMS Key CFT created
    * Allows Account's Root to administer the key
	* Allows IAM Role to use the key for S3 Bucket
  * EC2 Instance CFT created.
  * S3 Bucket CFT created
    * Encrypt the bucket using its KMS Key
	* Containing a Bucket Polcy that allows the IAM Role to use it and access its files.
  * IAM Policy CFT created
    * Allows the IAM Role to access the S3 Bucket
	* Allows the IAM Role to access the KMS Key
	
This is the Linux goals set from Olympus:
  * Create a new user named "Tullius"
  * The user "Tullius" must have sudo access without needing a password
  * Inside "Tullius" Home Directory, create a directory named "files".
  * Inside /home/Tullius/files directory, create 100 empty files.
  * Send all 100 files to the S3 Bucket created.

## Twisted Goals:
  * You cannot use resources given to you from the project. Everything must be made on your own.
  * All resources must be created from a pipeline!
    * The pipeline must be created using a CFT.
	  * This CFT must reside: GitRepo:/cicd/Solitude/Corp5-TES-Solitude-Pipeline.yml
	* All Cloudformation template files must reside: GitRepo:/iac/Solitude/cft/Corp5-TES-Solitude-*.yml
  * The pipeline must contain two environments:
	  * All "Development" configuration template files must reside: GitRepo:/iac/Solitude/var/dev/Corp5-TES-Solitude-Dev-*.json
	  * All "Release" configuration template files must reside: GitRepo:/iac/Solitude/var/release/Corp5-TES-Solitude-Release-*.json
    * Approval Stages are required prior to the deployment stages (Dev / Rel Stages)
  * All resources that was given is considered "Shared" resource and must be used by both deployment environments.
    * You must create the VPC, Subnets and ensure Session Manager works with the EC2
    * You must create the key pair.
    * You can use any of Amazon's free AMI that supports Session Manager.
  * All Linux commands must be done automatically.
    * Use the "UserData" from the EC2 Cft
      * Due to complications, This would just be a manual check.
        * Userdata script runs new shells as root, even if you su into another user. using $(command) will not work as intended due to this issue. eg `$(whoami)` will be root even if you run `su - ec2-user -c 'echo $(whoami) > ~/whoami.txt'
        * On that note, using su correctly does allow you to change the current shell into the user. eg running `su - ec2-user -c 'mkdir ~/hello_world; echo "Hello, World!" > ~/hello_world/README.txt' will still do everything inside ec2-home directory.
        * Lastly, we could still test sudo for Tullius by sudoing the aws command to upload 100 files. If the 100 files upload (As in, no password check), then the user's sudo permission was done successfully.

