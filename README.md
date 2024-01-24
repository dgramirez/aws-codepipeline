# Derrick's AWS Codepipeline

This is a simple repository, connected with an AWS Codestar to show off some things I've done
with AWS Codepipeline.  

I will be placing Cloudformation Template Files (in YAML) & Cloudformation Configuration Files.  

For Consistency Sake, I will be doing the following:  
  * If it is possible to place tags on the resources, Then it must be done in this fashion:
    * Organization: Corp5
	* Team: TES
	* Application: [Project Name]
	* Purpose: [Very Short & consice description, no more than 8 words]
	* Environment: Dev or Rel
	
  * For Resource Names, it should follow: {Organization}-{Team}-{Application}-{Environment}-{Resource Name}
    * For {Resource Name}, it can follow the following format: {Desired Category}-{Resource Category}-{Resource Type}
	  * Desired Category or Name: [CONDITIONAL] A User-Chosen Name / Category. This is only used if you need two or more of the same resources.
	  * Resource Category: [REQUIRED] This is the category that the resource will be using (eg. ec2, s3, kms, rds, etc.)
	  * Resource Type: [REQUIRED] This is the actual resource type (eg. bucket, policy, dbinstance, key, etc.)
