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

**Build Linux webserv VM**
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
- Recovery point is to which date/time can the data be recovered<br/>
There are different snapshot types:<br/>
  - Application consistent
  - File System consistent
  - Crash Consistent

**Lab for backup Service for VM**
- During creating the vm, it is possible to Enable a backup(all of backup data will be stored in recovery service vault) or after creatting vm
- Backup policy: the configuration is going to be define here

**Recovery Service Vault**: is used for backup or site recovery(vm replication)

**Enable Site Recovery or Disaster Recovery for VM**
- The site recovery service extension is installed on source vm
- Continous replication is occuring via the cache storage account
- when the data is processed in the target region, crash consistent recover points are generated every 5 minutes
Info: All of the data on the vm are sent to cache storage account, and the data are transfered in the target region
Once you have a retention point on the target region, you can do failover
There two typs of recovery points:
- Crash consistent: if you recovery to a near time in the past, then you need crash consistent snapshot
- Applications consistent: if you need to recovery all apps at certain time

**Availability set** 
- Protect your infrastructure from update or maintaince on physical server of MS.
- The only to assign availablity set to vm is during the creation of vm. It is not possible to assign an existing vm with an availability set
- There is max 3 fault-domains and max 20 update domains

**Azure Disk Encryption**
You use ADE to encrypt a data on the disk of vm. You will need a key vault to encrypt and decrypt the data.
By Creation you need:
  - In "Access Policy" choose Azure Disk Encryption for volume encryption (VM will check if this policy enabled if yes it will create and use encrpytion key)
  - Select permissions in created row data in list down (encrypt, decrypt, unwrap,...)
  - After creating keyvault, run this cmd(this will encrypt you c and d drive or all drives) <br/>
  cmd: az vm encryption enable -g azuredemo --name keyvm --disk-encryption-keyvault demovault9000 <br/>
  Info: It takes around 15 minutes for execution. You have to see a lock-Symbole after execution

**Azure Web App**
Man deploy web apps by azure web app. If you use azure web app to deploy an app, then you need first **azure app service plan**. Azure Web App is as PaaS and can deploy many programming language(java, node js, c#,...).
There are various azure service plan and pricing: here is more *[Info about pricing](https://azure.microsoft.com/en-us/pricing/details/app-service/windows/)*

