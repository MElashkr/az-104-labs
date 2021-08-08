# Configure and manag VNET

## ARM
This provide the ability to define your infrastructure as a code. You create a template using JSON(Javascript objects Notation). This defines the configuration and deployment that need to deploy to azure. <br/>
A Json-File can be used to create a vm, storage account, virtual network, etc.
There are different sections: <br/>
- **Resources**: is used to specifiy the resource to deploy
- **Variables**: are values that can be used in the template 
- **Paramteres**: can be used to to provide values in the deployment phase
- **Output**: this returns values from the deployed resources

## Loadbalancer
It will be used to manage and distrubute the traffic between comming requests from users and virtual machines. It is actually as a part if vm <br/>
**Loadbalancer**
- Backendpool: Need to know what are the target vms which can direct the request to them(assign/add the vms that are going to bind to loadbalancer)
- Frontend-IP is the public-ip address of the loadbalancer
- Health-probe will be used to know whether the backend vms are healthy or not
- Loadbalancer rules: define how the traffic will be forwarded to which port on virtual network

**There are 2 types of SKUs LB(pricing)**
- Basic LB
  - For a singl vm
  - Has availability set
  - Scale set

- Standard LB
  - For multiple vms
  - Has availability set
  - Scale set
  - High SLA of 99.99
  
  **There are two types of LB**
  - Internal LB: it is internal to your network
  - External LB: is exposed to the internet

Note: if you have multiple vms und you want to set up a load balancer, then these vms need to be as part of availability set or vm scale set

**Inbound NAT rules**
When man needs to path specific requests(on specific port) to pass it to a loadbalancer on vms.
Info: you choose the port which a request is comming from outside and and adapt it to a cusom prot mapping and choose target port of vm<br/>
Info: it is still required, that you allow RDP-Protocol on port 3389 on the vm in Network section.



