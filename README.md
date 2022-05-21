# Application-Security-Groups

# What are Application Security Groups (ASG)?
- ASGs is like an extension to Network Security Groups.
- To make security more tighter, ASGs allow IT admins to easily specific a source and destination when it comes to filtering traffic in the NSGs.


- Instead of specifying a Source IP address within inbound rules, admins can add Virtual Machines to a Application Security Group. 
- This is useful for companies with 1000s of virtual machines. 



# Why is it useful?
- If a company has a collection of servers where one VM is hosting an application and another VM hosting a database, admins would have to add the private IP of each server instance in the allow rule. 
- Instead of manually adding private IP of each servers into the inbound rule of NSGs, put them into ASGs.
- Then configure the Network Security Group's inbound rules and add the ASG that contains all the machines to allow.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169555420-4c0df506-7534-45a9-a978-1a7212723a18.png" height="290%" width="290%" alt="review of vnets and VMs"/>

<p/>


# Use Case: Use Application Security Groups for host VMs to access a SQL server
- Download Microsoft SQL Management Studio onto one VM - Application Server
- Download SQL Server onto the Database server
- Connect application server to the database server.
- Add the VMs acting as servers into the application security groups instead of NSGs.
- Allow traffic from ASG within the NSG.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169555347-2eddc451-7a70-4017-bf6c-f6a04c8f4438.png" height="290%" width="290%" alt="review of vnets and VMs"/>

<p/>


# How to set up an Application Security Group?


<p align="center">
  
<img src="" height="290%" width="290%" alt="ASG demo"/>

<p/>

# ASG Setup: RDP into <em> demoVM </em> download SQL serever management studio on the <em> demoVM </em>
- Before downloading Management Studio, ensure that IEE Security Configuration is turned off.
- Local server > IEE Security Configuration > Turn off both 
- Download and install SSMS

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169664409-e39483f9-f7e1-4062-9341-6189ffa43623.png" height="290%" width="290%" alt="ASG demo"/>

<p/>



# ASG Setup: RDP into <em> databaseVM </em> and download Microsoft SQL Server on <em> databasevm </em>
- Before downloading SQL Server, ensure that IEE Security Configuration is turned off.
- Local server > IEE Security Configuration > Turn off both 
- Download and install SQL Server Free Trial EXE 64-bit edition
- Custom > Install > Installation > New SQL Server stand-alone installation or add features...
- Select next until Database engine and select the DB engine > Mixed Mode ? Provide Password to access SQL server and add a admin user

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169665186-23f23035-8bdc-4a0d-b361-e6ec8e4d9eeb.png" height="290%" width="290%" alt="ASG demo"/>

<p/>

# Accessing the SQL Server
- Admins must configure Windows Firewall Advanced and add an Inbound Rule
- Windows Defender Firewall > Inbound Rules > Add New > Custom > Next > Change to TCP > Specific ports > 1433 
- Microsoft SQL Server listens on port 1433

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169666052-b272080e-b95f-49a1-b27c-1e3dbf8979ce.png" height="290%" width="290%" alt="ASG demo"/>

<p/>


<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169666072-70daeaba-12c6-4c73-b19e-2b6792300ad2.png" height="290%" width="290%" alt="ASG demo"/>

<p/>
