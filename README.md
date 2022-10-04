# Application-Security-Groups

# What are Application Security Groups (ASG)?
- ASGs is like an extension to Network Security Groups.
- To make security more tighter, ASGs allow IT admins to easily specific a source and destination when it comes to filtering traffic in the NSGs.


- Instead of specifying a Source IP address for hundreds of inbound rules, admins can add Virtual Machines to a Application Security Group. 
- This is useful for companies with 1000s of virtual machines. 



# Why is it useful?
- If a company has a collection of servers where one VM is hosting an application and another VM hosting a database, admins would have to add the private IP of each server instance in the allow rule. 
- Instead of manually adding private IP of each servers into the inbound rule of NSGs, put them into ASGs.
- Then configure the Network Security Group's inbound rules and add the ASG that contains all the machines to allow.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169555420-4c0df506-7534-45a9-a978-1a7212723a18.png" height="290%" width="290%" alt="review of vnets and VMs"/>

<p/>


# Use Case: Use Application Security Groups for host VMs to access a SQL server
- Download Microsoft SQL Management Studio onto one server - demovm 
- Download SQL Server onto the Database server - databasevm
- Connect demovm server to the database server.
- Add the VMs acting as servers into the application security groups instead of NSGs.
- Allow traffic from ASG within the NSG.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169555347-2eddc451-7a70-4017-bf6c-f6a04c8f4438.png" height="290%" width="290%" alt="review of vnets and VMs"/>

<p/>


# How to set up an Application Security Group?

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

- Then navigate to Microsot SQL Server 2019 Configuration Manager
- SQL Server Network Configuration > Protocols for MSSQLSERVER > TCP/IP > IP Addresses > Select <em> Yes </em> for enabled and apply


<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169666864-dbe70d52-4842-4dcb-8c2c-8d47f2c4b3d9.png" height="290%" width="290%" alt="ASG demo"/>

<p/>

# How to restart SQL Server Services 

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169666918-582fc574-6070-456f-9e8f-111c96c33bc9.png" height="290%" width="290%" alt="ASG demo"/>

<p/>



# Application Security Groups - Implementation
- Now, from Databasevm, admins must control inbound traffic.

# Adding inbound rule in databasevm
# Use Case: Deny all traffic onto database VM
- Below is an inbound rule that denies all traffic. 
- The deny rule trumps the allow traffic rule within Vnet due to priority rankings

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169667553-1592c6c8-803e-4914-aeba-033123beaf98.png" height="290%" width="290%" alt="ASG demo"/>

<p/>

# Remember, in order to access the SQL server, admins must use admin credentials that was created.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169721898-4da27189-c991-4036-aeb9-db8ec1a83b4f.png" height="80%" width="80%" alt="ASG demo"/>

<p/>

# If admins are unable to log in, username entered may be correct. Use "sa" as username and enter the password that was created.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169721940-95f7023f-eb51-4063-9b2e-dd3d17149fa7.png" height="80%" width="80%" alt="ASG demo"/>

<p/>

# Use Case: Allow demovm to access databasevm using inbound rule
- Take private IP of demovm and add it as a source to the inbound rule for databasevm
- Take private IP of databasevm and add it as a destination to the inbound rule for databasevm

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169668048-b3526efa-174d-428a-aa05-bb08a0e48c97.png" height="76%" width="76%" alt="ASG demo"/>

<p/>

# Use Case: Implement Application Security Groups
- Imagine if you had hundreds of <em> demovm </em> and had to add all the private IPs of each VMs into an inbound rule for an NSG.
- Instead, Admins can use application security groups and then add those VMs to the app sec group.

# Create ASG

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169668877-133e1dfe-8725-4e9a-863e-4bfca941a608.png" height="180%" width="180%" alt="ASG demo"/>

<p/>

# Link the Application Security group to the demovm NIC. 
- For companies that have hundreds of VMs, admins can link those vms to the ASG.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169669623-f0baf5f8-fc63-4e77-a92c-f7d4c9c9df0d.png" height="250%" width="250%" alt="ASG demo"/>

<p/>

- Instead of mentioning the private IP of demovm, add the ASG, which already has demovm inside of it.

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/169670526-cefc07c5-68f3-4bef-b31a-4e6bf91cbc9e.png" height="250%" width="250%" alt="ASG demo"/>

<p/>




