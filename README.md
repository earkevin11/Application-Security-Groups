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
  
<img src="" height="290%" width="290%" alt="review of vnets and VMs"/>

<p/>



