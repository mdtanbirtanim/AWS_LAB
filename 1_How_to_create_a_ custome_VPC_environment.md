# How to create a custome VPC environment in AWS

## Step 1: On AWS Account
    
    Login to your AWS console and select Region (We considered "Tokyo").
	Navigate to the VPC, On the VPC Dashboard, select Your VPCs, and  then select "Create VPC".
	In Name tag, We considered the name of VPC as "awslab", in IPv4 CIDR block, we entered "10.0.0.0/16", & then select "Create VPC".

    NB: We left "Tenancy" to default

## Step 2: Create Public & Private Subnet
    We are going to create 2 Public Subnets & 2 Private Subnets
    On the Subnet page, select "Create Subnet"
    In VPC ID, select "awslab"

    For Public Subnet 1, we considered following 
        Subnet Name: Public Subnet 1"
        Availability Zone: "ap-northeast-1a"
        IPv4 CIDR block: "10.0.0.0 /24"  > Then select "Create Subnet"

    For Public Subnet 2, we considered following information
        Subnet Name: "Public Subnet 2"
        Availability Zone: "ap-northeast-1c"
        IPv4 CIDR block: "10.0.1.0/24" > Then select "Create Subnet"
        
    To enable auto-assign piblic IPv4 address follow the below  procedure (NB: Applicable only for public subnet)
         Click on "Public Subnet 1" check box > "Action" >  "Edit subnet setting" > Do Tick mark on "Enable auto-assign public IPv4 address" > "Save"

    For Private Subnet 1, we considered below information
        Subnet Name: "Private Subnet 1"
        Availability Zone: "ap-northeast-1a"
        IPv4 CIDR block: "10.0.2.0/24" > Then select "Create Subnet"

    For Private Subnet 2, we considered below information
        Subnet Name: "Private Subnet 2"
        Availability Zone: "ap-northeast-1c"
        IPv4 CIDR block: "10.0.3.0/24" > Then select "Create Subnet"

Resourses:
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#subnet-basics
- For Subnet Creator https://network00.com/NetworkTools/IPv4SubnetCreator/
- For CIDR Range https://cidr.xyz/

## Step 3: Create an Internet Gateway (IG)

    On the VPC Dashboard, Navigate to Internet Gateways and select "Create internet gateway".
	In Name tag we considered "awslab IG", and then select "Create internet gateway".

	After creating IG, do following paths
        Navigate to IG > Select "awslab IG" check box >
        Select Actions > Attach to VPC > In Available VPCs, select "awslab" > Attach internet gateway.
## Step 4: Create a NAT gateway

    In this phase we are going to create 2 NAT Gateways to allow communication out of the private subnets.

    On the VPC Dashboard, in the navigation pane, select "NAT Gateways".
    Select "Create NAT gateway".
    In Name, we considered "awslab Gateway 1" > then in Subnet, select "Public Subnet 1".
    Select "Allocate Elastic IP (Public IP) > then select "Create NAT Gateway".

    For 2nd NAT, go again In navigation pane, select "NAT Gateways", and then select "Create NAT gateway".

    In Name, enter "awslab NAT Gateway 2".
    In Subnet, select "Public Subnet 2".
    Select "Allocate Elastic IP" (Public IP), > then select "Create NAT Gateway".

## Step 5: Configure the public route table

    Configure the public route table

    On the VPC Dashboard, in the navigation pane, select Route Tables.
    Expand the VPC ID column, locate the route that has a awslab > then select the check box for the awslab row.
        1. select the Routes tab.
        2. Click Edit routes 
        3.  "   Add route
        4. 
        5. In Destination, enter 0.0.0.0/0
        6. 
        7. In the Target drop-down list, select Internet Gateway > 
        8. click  the "awslab IG".
        9. Save

	Now associate "Public Subnet" into "Public RT"
		1. Click on "Subnet Associations"
		2.   "	on "Edit subnet associations"
		3. Do tick mark on "Public Subnet 1 & Public Subnet 2 check box"
		4. Click "Save Associations"
        
## Resources
- https://docs.aws.amazon.com/vpc/index.html
- For Subnet Creator https://network00.com/NetworkTools/IPv4SubnetCreator/
- For CIDR Range https://cidr.xyz/