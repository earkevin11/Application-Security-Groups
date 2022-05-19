# Application-Security-Groups

# What are Application Security Groups (ASG)?
- ASGs is like an extension to Network Security Groups.
- To make security more tighter, ASGs allow IT admins to easily specific a source and destination when it comes to filtering traffic in the NSGs.
- Ex: If a company has a collection of servers where one VM is hosting an application and another VM hosting a database, admins would have to add the private IP of each server instance in the allow rule. 
- It's tedious. Instead of manually adding private IP of each servers, put them into ASGs.
- Instead admins can use Application Security Groups.




- Instead of specifying a Source IP address within inbound rules, admins can add Virtual Machines to a Application Security Group. 
- This is useful for companies with 1000s of virtual machines. 


# Use Case: Use Application Security Groups for host VMs to access a SQL server


# How to set up an Application Security Group?
- 
