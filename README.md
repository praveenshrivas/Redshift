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
- Tag (Key - Name & Value - EC2-SQL-Client)



** Provision EC2 for data Generation**

