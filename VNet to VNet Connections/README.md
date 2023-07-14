---

<h1> V-Net to V-Net Connections in Azure </h1> </br>

By deploying a VPN Gateway into a dedicated "gateway subnet" of our virtual networks, we can create one or more encrypted tunnel connections between the VPN Gateway of our Azure V-Net and any of the following:
other virtual networks (VNet-to-VNet connections)
our on-premises VPN device (Site-to-Site connections)
the client devices of our remote workers (Point-to-Site connections)

The VPN Gateway can be combined with other Azure networking services to provide us with more advanced solutions, such as functioning as a Gateway Transit to support routing in a Hub and Spoke network topology. It supports multiple protocols and provides options for various bandwidth speeds and high availability, subject to pricing based on the Gateway SKU that is selected for deployment.
Over the weekend, I had an opportunity to lab up each of these different VPN gateway connection types (with limitations) using the Azure Portal. In this article, I discuss how I was able to bridge the connection between my two Azure Virtual Networks by creating a VNet-to-VNet connection with the use of VPN Gateways (tutorial source: Microsoft.com). I was able to accomplish this by completing the following steps:
Source: Microsoft.comCreating and configuring VNet1
Creating the VNet1 gateway
Creating and configuring VNet4
Creating the VNet4 gateway
Configuring the VNet1 gateway connection
Configuring the VNet4 gateway connection
Verifying my connections

---

Create and Configure VNet1 and VPN Gateway 1
In the first step, I created the first virtual network, VNet1, for this scenario. It is part of the TestRG1 Resource group and is located in the East US Azure Region.
Configuration of VNet1Next, I configured the IP addressing needs for the network, providing it with a network address space and a FrontEnd subnet taken from this address space.
Configuration of Subnet on VNet1With the VNet1 virtual network in place, I then deployed a VPN Gateway to a dedicated gateway subnet within the VNet1. Microsoft recommends that it is best practice to use a CIDR/27 address block to allow for future expansion. The gateway is of type VPN and is Route-Based. I did not enable any of the High-Availability options or BGP for this deployment.
The selected gateway SKU is among one the lower-priced options and it offers a lower bandwidth throughput than some of the other higher-priced options. You can find more information about VPN Gateway settings, feature sets, and capabilities based on SKU here.
Create VPN Gateway for VNet1

---

Create and Configure VNet4 and VPN Gateway 4
With everything in place for VNet1, I then configured the virtual network for VNet4 and this one is located in the West US Azure Region.
Configuration of VNet4Here, I configured the address space for VNet4 and a FrontEnd subnet range taken from the network address space.
Configure subnet on VNet4Subnet added to VNet4Next, I deployed a VPN Gateway for the VNet4 virtual network. This one is also a Route-based VPN type gateway deployed to a dedicated gateway subnet within the VNet4 virtual network.
Configure VPN Gateway for VNet4Here, we have both VPN Gateways configured for both VNet1 and VNet4.
VPN Gateways were created for both VNet1 and Vnet4

---

Configure the Gateway Connections
The next phase of the configuration involved configuring the VNet-to-VNet Connection from each VPN Gateway. From VNet1GW, I created the connection and associated it with VNet4GW, which is on the remote end within the gateway subnet of VNet4. Here, I supplied the gateway with a Shared key that must match the connection when it gets configured on the remote end in order for connectivity to be established. Here we selected IKEv2 as the tunneling protocol, as it is the most recent of the two in regards to VPN protocols. It is fast and very reliable when switching between networks.
Add VNet-to-VNet Connection from VNet1 to VNet4Next, I configured the connection from VNet4's VPN gateway to VNet1's gateway and associated the two VPN Gateways here. Here, I entered the Shared Key, which is required to match the key that was provided from the other end of the connection when it was created on the VNet1 side. Here we selected IKEv2 as the tunneling protocol, as it is the most recent of the two in regards to VPN protocols. It is fast and very reliable when switching between networks.
Add VNet-to-VNet Connection from VNet4 to VNet1Finally, I verified that the VPN Gateway Connection is in a "Connected" status from both ends of the link. This is from the perspective of VNet4.
Verification of "Connected" status for VNet-to-VNet Connection from VNet4As a final step, I then verified the "Connected" status of the VNet-to-VNet Connection from the perspective of VNet1.
Verification of "Connected" status for VNet-to-VNet Connection from VNet1I enjoyed configuring both the VPN Gateways and the VNet-to-VNet Connection for the two virtual networks in this lab and I found it fairly simple to accomplish. I also enjoyed learning more about the additional capabilities that are available by using VPN Gateways in our architecture in order to enable communication between Azure Virtual Networks or between Azure VNets and on-premises networks for hybrid networking solutions.
Thank you for reading!
References:
