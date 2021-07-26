## Deploy VM

![alt text](https://github.com/MElashkr/az-104-labs/blob/main/Pictures/deploy-vm.JPG?row=true "Deploy vm")

To deploy vm, you need
- Virtual network
- Disk that assigned to vm
- Network interface that assigned to vm
  - All packages, that are sended from and to vm, are going through Network interface
- Network Security group is like a firewal which decide which type of traffic are going into vm

**Issue which is coming by connecting to vm:**
- Maybe you get an error username or password is not right
you can type by username: ip\username and your password
fx. username: 12.134.45\username
    pw: temp
  
**Connect to azure-vm**
- Install iis on azure vm: you install iis as a role by Manager dashboard on installed windows server in vm
- Add inbound rule in Networking-Section to connect to vm(or iis) from outside
  - choose TCP and port 80
- Don't store important data on temproray disk
  - Because data on temporary disk is lost during maintenance event
  - Data is lost when you redeploy the vm
- If you restart the vm, the public-ip address remains as it is
- If you stop/deallocate the vm, the public-ip will be lost

** Build Linux webserv VM**
- use putty to Connect to vm
- **insall iis**<br/>
// update package index<br/>
cmd: sudo apt-get update<br/>
// install ngix tool<br/>
cmd: sudo apt-get install ngnix<br/>
Info: nginx will be run on port 80 and we need to create a role for vm to allow traffic on port 80<br/>
Step: add inbound role in azure in Networking-Section of vm
Source: service tag, Destination port range: 80


**Snapshots**
That can be used to make a backup from an OS or Data on the disk

**Shared Disk**
That allows you to attache a managed disk to multiple vms. That can be enabled only for **Premium and Ultra Disk**

- Lab:
  - Create a shared Disk with Min-Share >=2
  - Attach created Disk during creating a vm 
  - To get the Disk enabled to vm
    - Go to VM on File and Storage Services, then **Initialize and Create New Volume**

**Custom Script Extension**
Run script on vm. you need:
- Azure Storage account(ASA) to upload script files
- Run script files in Extension-Menu of VM in Azure-Portal from ASA, script-files could be f.x install iis-server on vm

**Run Command in vm**
It is possible to run powershel commands on vm by Azure-Portal

**Azure Backup Service for vm**
Man can do a backup of vm-file or Disk, and this backup will be stored in Azure Recovery Vault
There are Retention Time and Recovery Point
- Retention time captures how long the data can be retained (f.x one week or one month)
- Recovery point is to which date/time can the data be recovered
There are different snapshot types:
- Application consistent
- File System consistent
- Crash Consistent

**Lab for backup Service for VM**
- During creating the vm, Enable a backup(all of backup data will be stored in recovery service vault)
- Backup policy: the configuration is going to be define here

