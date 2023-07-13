As I am progressing in my Microsoft Azure studies, I am learning more about the different networking capabilities that the service offers for establishing connectivity to our virtual networks (VNets)that are hosted in the Azure cloud. For intersite connectivity options, Azure offers several options that can be used alone or in various combinations to achieve simple (Azure-to-Azure) or more complex (Azure to On-premises) solutions.

Now, there are various types of Azure resources that we can deploy into our Virtual Networks and by using VNets we are able to communicate between these Azure resources. Well, sort of. Virtual Networks are isolated from other Virtual Networks in the Azure Cloud. So this means that if I deploy virtual machines (VMs) into multiple VNets, only those VMs that live in the same VNet will be able to communicate with each other, thanks to the automatic system routes.

While all resources in a VNet have the ability to communicate outbound to the Internet, by default, there are some additional configuration steps that need to be taken to allow: 1) communication between different VNets 2) communication with on-premises networks and 3) inbound communications from the Public Internet.


Diagram of my lab scenario
In this lab, I was able to practice this scenario (source: Kodekloud) of configuring the easiest solution for implementing intersite connectivity between different Azure VNets, Virtual Network Peering!!

Per Microsoft’s online documentation, we have the options for virtual network peering within the same region or we can opt for global network peering, where needed. Each option has a different rate for inbound and outbound data transfers based on the region where your VNets are deployed. There are many benefits to peering for connecting our virtual networks, such as low latency, high bandwidth, and private connectivity between our resources in different virtual networks.

The following steps were taken to allow me to implement VNet Peering:

Created two virtual networks
Deployed a virtual machine (VM) into each virtual network
Connected two virtual networks with a virtual network peering
Tested communication between the VMs
Deploying the Infrastructure (Steps 1–2)
I accomplished steps 1–2 by using a PowerShell script to quickly deploy my network infrastructure. In this deployment, we have two virtual networks, eus-vnet and wus-vnet, each deployed to different Azure Regions (East US and West US 3). We also have two virtual machines (eus-prod-server and wus-prod-server) both with Linux Ubuntu as the OS image. A public IP address was configured for the East US server to allow me to connect to it over the public Internet. A public IP address is a requirement in order to allow any Azure resource to receive inbound communication from the Internet. Both servers have private IP addresses that were assigned by Azure, taken from the address space of the virtual network subnets where the VMs were deployed to.


Network infrastructure deployed using a PowerShell script

Two virtual machines deployed to two different virtual networks
The East US server has a Public IP address of 52.149.224.175 and a private IP address of 10.0.0.4. This is the server that I will connect directly to from my PC over the public Internet.


Virtual machine (eus-prod-server) deployed to East US region
The West US server does not have a public IP address. Therefore, we are not able to connect to it directly from the Internet, but we will utilize our connection to the East US server and from that server, we will be able to connect to the West US server. The wus-prod-server has a private IP address of 192.168.1.4.


Virtual machine (wus-prod-server) deployed to West US 3 region
Next, I launched my SSH client to establish a connection from my PC to the server located in East US and I logged in using the credentials that I specified in the PowerShell script.


Using Putty SSH client to connect to eus-prod-server @52.149.224.175

SSH connection to eus-prod-server is established
By default, this virtual machine will have outbound connectivity to the Internet, as demonstrated in my ping out from the VM to Google’s DNS service, 8.8.4.4.


My next test was a ping out to the private IP address of the server located in West US (wus-prod-server ) @ 192.168.1.4. However, I did not receive any replies from the West US prod server, as indicated in the image listed below. This was expected because I know that the two servers are located in different virtual networks. As mentioned earlier, Virtual Networks in Azure are isolated from each other and we must apply additional configuration in order to allow this communication to take place between them. This is where the VNet peering comes into play that can help us to bridge that communication in order to get the two VNets connected so that their resources will be able to communicate with each other.


3. Create the Virtual Network Peering Connections
From the Virtual Network located in the West US region (wus-vnet), I navigated to the “Peerings” blade in order to set up this peering connection.


West US Virtual Network blade
From this peering configuration screen we see a message indicating that “For peering to work, two peering links must be created. By selecting remote virtual network, Azure will create both peering links.” This means that we must have a link created between both ends of the virtual networks in order for them to peer to each other. However, we find that Azure creates the remote end connection for us once we have completed the configuration on the first VNet, wus-vnet. Well, it does so when creating a peering link from the Azure Portal versus creating them from the Azure CLI.

On this peerings configuration screen, we are creating it from the wus-vnet. Therefore, the initial peering link listed below is referring to the West US VNet and we appropriately named it “west-to-east”.


Once we scroll down on this screen, we now need to provide information about the remote virtual network by selecting it from the list. Here we named the remote virtual network peering link “east-to-west”. Click on Add


Once the creation process was completed, I was able to refresh the screen on the wus-vnet’s “Peerings” blade and my local link from this West US virtual network displayed a Peering status of “Connected”.


Connected link from West US to East US Virtual Networks
I then made my way over to the Peerings page of the East US Virtual Network (eus-vnet) and found that the Peering Status of the remote link was also in a “Connected” status.


Connected link from East US to West US Virtual Networks
4. Testing Communication Between the Virtual Machines
After confirming that I had a connected peering link from both virtual networks, from East US to West US and from West US to East US, I then tested my connectivity from the eus-prod-server to the wus-prod-server, and this time my connectivity test was successful!! I received replies from the server wus-prod-server @ 192.168.1.4 as per the image below.


With my testing completed successfully, I was able to confirm that Virtual Network Peering can help me to enable private connectivity between two Azure-to-Azure resources when I need this communication to take place between two resources that live in different VNets on the Azure Cloud.

Finally, I made sure to clean up by deleting all resources from my Azure subscription that are no longer needed so that I won’t incur any billing for things that aren’t needed. Please make sure that you do the same if you are practicing labs in your own Azure environment.


Deleting resources that are no longer needed

