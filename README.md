>># Installing and Configuring Ansible on AWS Ec2 Machine 

>## Project Description

- Ansible is a agentless configuration management tool used to automate tasks and provide continous delivery of applications. 
- This project involved setting up an EC2 virtual machine used as a jump server to control declared servers and perform tasks with the help of Ansible. 
>### Project Diagram 
![](/PNGs/Project%2011%20Diagram.png)

>### Step One 
- spin up Ec2 machine and install Ansible 
    - sudo apt update
    - sudo apt install ansible
>### Step Two 
- Set-up a freestyle project and configured webhook to trigger ansible build
- configured post-build job to save all files.
- Cloned repo 
![](PNGs/3.%20Clonning%20Repo%20.png)
- setting up ansible directories (inventory, playbooks, common, prod, dev. uat)
- Tested setup and checked builds in the directory running the command :
  - ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/

>### Step Three
1. Set up SSH-Agent on Host PC 
-    eval `ssh-agent -s`
-    ssh-add <path-to-private-key>
![](/PNGs/5.%20pem%20key%20added%20to%20ssh%20agent.png)
2. Confirming the key was added 
-    ssh-add -l
3. SSH into instance using the code: 
-    ssh -A ubuntu@public-ip
![](PNGs/6.%20SSH%20using%20Agent.png)
>### Step Four 
1.  Creating Playbook Directories and updating with Hosts, tasks 
    -  [nfs]
    - <NFS-Server-Private-IP-Address> ansible_ssh_user='ec2-user'

    -  [webservers]
    - <Web-Server1-Private-IP-Address> ansible_ssh_user='ec2-user'
    - <Web-Server2-Private-IP-Address> ansible_ssh_user='ec2-user'

    -  [db]
    - <Database-Private-IP-Address> ansible_ssh_user='ec2-user' 

    -  [lb]
    - <Load-Balancer-Private-IP-Address> ansible_ssh_user='ubuntu'
![](PNGs/7.%20Editing%20inventory-dev%20directory.png)

2. Updating playbooks/common.yml directory 
![](PNGs/8.%20Updating%20Common.yml%20directory.png)

>### Step Five
1. Pushing Changes to github branch
![](/PNGs/9.%20Pushing%20changes%20to%20branch%20.png)

>### Successfully ran playbook 
![](PNGs/11.%20Successful%20SSH%20from%20controller%20server.png)

>### Confirming Wireshark installed on target host server
![](PNGs/12.%20Checking%20wireshark%20version%20on%20NFS-server.png)
