# Redshift


**Services we need to create in Advance.**


1. IAM User (Optional)
   Genrally, it is recommended to use IAM user for daily Task.
	- with Web Console Access
	- either with full admin previledges 
	- or with Redshift, EC2, S3, Cloudwatch full access
	
2. Roles
   We Need two roles, one for EC2 Instance another for Redshift.
	- For EC2 (Choose S3FullAccess Policy)
	- For Redshift (Choose S3FullAccess Policy)

3. VPC
   You can choose VPC wizard to create the VPC.
	- Where your Redshift cluster will run 
  - Choose the option VPC with single public subnet

4. EC2
   We need two Instances. (one where our SQL Client will be installed and Another we will be using for the data generation.)
	- EC2 SQL Client - postgresql
	- EC2 Data Generator (As we aere not having data in advance to process)
  
5. S3 Bucket
   Create one S3 bucket where we will keep our Data which we have generated from Data Generator Instance. 
  

**Provision EC2 Instance for SQL Client**

- Choose Amazon linux with t2.micro Instance type
- Associate the role which we have created for s3
- Root volume - keep it default 
- create Security Group - Choose port 22 for SSH
- Tag (Key - Name & Value - EC2-SQL-Client)
- Login to putty and install SQL Client and git 

Use the command 
- 	yum update 
- 	sudo yum install postgresql git 


** Provision EC2 for data Generation**
- Choose Amazon linux with d2.xlarge Instance type
- Associate the role which we have created for s3
- Root volume - 200 GB
- create Security Group - Choose port 22 for SSH
- Tag (Key - Name & Value - EC2-Data-Generator)

Use the below command to generate random data 

- sudo yum install gcc make flex bison byacc git
- git clone https://github.com/gregrahn/tpcds-kit.git
- cd tpcds-kit/tools
- make OS=LINUX
- cd $HOME
- git clone https://github.com/sko71/hands-on-with-redshift.git
- mkdir tpcds
- ls -l
- cd hands-on-with-redshift/
- ls -l
- vi datagen.sh (you can see the data Generation script here)
- chmod +x datagen.sh
- nohup ./datagen.sh & (this will run the command in backgrouda and generate random data)
- ps -ef|grep dsdgen (you can see if the process is running or not)

It will take around 2 hours to generate the random data. 


- cd $HOME/tpcds (you can see the files here after two hours)
- cd $HOME
- cd hands-on-with-redshift/
- vi copy_files.sh (replace the bucket name with your bucket)
- chmod +x copy_files.sh
- nohup ./copy_files.sh & (it will push the files from EC2 to the S3 bucket)

It will take around 30 minutes. 

