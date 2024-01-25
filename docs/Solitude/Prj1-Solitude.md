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
  * Inside "Tullius" Home Directory, create a directory named "Files".
  * Inside /home/Tullius/Files directory, create 100 empty files.
  * Send all 100 files to the S3 Bucket created.

## Twisted Goals:
  * You cannot use resources given to you from the project. Everything must be made on your own.
  * All resources must be created from a pipeline!
    * The pipeline must be created using a CFT.
	* This CFT must reside: GitRepo:/cicd/Solitude/Corp5-TES-Solitude-Pipeline.yml
  * The pipeline must contain two environments:
	* All Cloudformation template files must reside: GitRepo:/iac/Solitude/cft/Corp5-TES-Solitude-*.yml
	* All "Development" configuration template files must reside: GitRepo:/iac/Solitude/var/Corp5-TES-Solitude-Dev*.json
	* All "Release" configuration template files must reside: GitRepo:/iac/Solitude/var/Rel-Corp5-TES-Solitude-*.json
    * Approval Stages are required prior to the deployment stages (Dev / Rel Stages)
  * All resources that was given is considered "Shared" resource and must be used by both deployment environments.
    * You must create the VPC, Subnets and ensure Session Manager works with the EC2
    * You must create the key pair.
    * You can use any of Amazon's free AMI that supports Session Manager.
  * All Linux commands must be done automatically.
    * Use one "AWSUtility::CloudFormation::CommandRunner" to download the script from Github
	* Run the script for the remainder of the tasks
    * Record the following output and place it into the s3 bucket inside an "output" folder.
      * Send over /etc/sudoers for the sudo access
      * Cat the "ls -R /home/$(whoami)" into a file named "ls.txt"

