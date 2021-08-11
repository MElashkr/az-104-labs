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

## Application Gateway

Frontend-IP -> (App-Gateway/web-app firewall) -> Http(s)-Listner -> Rules -> (web-app on azure or on-premise)
Features:
- This service is as web traffic loadbalancer that is used to distribute traffic to web apps. 
- It is based on layer-7 on OSI.
- It supports SSL(Secure-Socket Layer Termination) (App-Gateway manages the communication for you)
- It is possible to Auto-Scale for App-Gateway resources and scale-up or scale-down based on traffic load pattern
- It is possible to enable Web-Firewall
- It is possible to enable session-Affinity. If the state of the user session will be saved on the server, then can be useful feature

Components of App-Gateway:
- Frontend-IP
- Http(s) Listner: that is logical entity that checks incomming connection requests. If a request is comming to a Listner, then it redirects this request to backend-pool. There can be multiple Listners attached to App-Gateway
  - There are 2 typs
    - Basic: the Listner listen to a single domain
    - Multiple side: the Listner listen to multiple domains
-  Routing roles: route traffic from the listner to backend-pool
  - There are two types of routing-pools
    - Basic: all requests will be routed to backend pool directly
    - Path: all requests will be routed to backend pool based on the URL
- Backend-pools: These can be Network-Interface Cards, Virtual machine Scale set, Public/Internal IP-Addresses, or Backend such as App-Service
- Health-Probs: how the App-Gateway will monitor the health of resources on the backend-pool

It is reachable through FrontendIP-Address. You manage traffic by defining Http/Https Listner and rules to route traffic to different endpoints(web-app on vm, web-app on Azure app service or web-app running on on-premise). It is important to have "Empty subnet" as a part of virtual network.
If you deploy App-Gateway, then will be deployed on Virtual network. <br/>
It is possible to enable web-app firewall to protect the app form corss-site scripting attack.<br/>
One other important thing, it is possible to route traffic based on URL (/videos, /images). Traffic will be routed based on the requests

**Azure Loadbalancer vs Application Gateway**
Loadbalancer will look at traffic based on Transport Layer(Layer 4), and App-Gateway will look at traffic based on Application Layer(Layer 7)
OSI-Layers:
7. Application Layer
6. Presentation Layer
5. Session Layer
4. Transport Layer(TCP-Protocol)
3. Network Layer(Hand-shake will be happen between source and destination machine)
2. Data Link Layer
1. Physical Layer
Data packets will be transport on the physical layer. Data will be converted to packetes and will be transported from source machine to destination machine.
Azure Loadbalancer will look only at transport layer(Layer 4)
Info: Wireshark tool to check and see the data packet that will be transported

It is possible to route monitor traffic which comming in/out from App-Gateway by Metric Session or Diagnostic settings. Man can anaylse Logs and send them to Log Analytics/Storage Account/Event hub 

## Virtual Network Peering
If you have 2 virtual network in 2 different regions and you want to connect each other, then you can bind them through network peering.
Once you enable virtual network peering between two virtual networks, the virtual machines can then communicate via their private IP addresses across the peering connection.

## Connecto to Azure vNet
**Point to site vpn-connection**
If you need to connect a workstation/clinet machine(on-premise) to virtual network on azure via private ip-address.<br/>
You need for connection:
- Root certificate(or self-signed certificate)
- User certificate with a private key & with public key
- Virtual network gateway
  - Gateway subnet
