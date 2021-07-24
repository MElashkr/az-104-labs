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

    
