As I progress in my Microsoft Azure studies, I am learning more about the different networking capabilities that the service offers for establishing connectivity to our virtual networks (VNets)that are hosted in the Azure cloud. For intersite connectivity options, Azure offers several options that can be used alone or in various combinations to achieve simple (Azure-to-Azure) or more complex (Azure to On-premises) solutions.

Now, we can deploy various types of Azure resources into our Virtual Networks, and by using VNets, we can establish connectivity between these Azure resources. Well, sort of. Virtual Networks are isolated from other Virtual Networks in the Azure Cloud. So this means that if I deploy virtual machines (VMs) into multiple VNets, only those VMs that live in the same VNet will be able to communicate with each other, thanks to the automatic system routes.

While all resources in a VNet can communicate outbound to the Internet, by default, some additional configuration steps need to be taken to allow: 1) communication between different VNets 2) communication with on-premises networks, and 3) inbound communications from the Public Internet.

<figure>
<img src="https://github.com/Nisha318/Microsoft-Azure-Projects/blob/main/Connecting%20Azure%20Virtual%20Networks%20Using%20VNet%20Peering/Lab%20Diagram.png" alt ="lab topology diagram ">
<figcaption> <b> Diagram of my lab scenario </b> </figcaption>
</figure>

In this lab, I was able to practice this scenario (source: Kodekloud.com) of configuring the easiest solution for implementing intersite connectivity between different Azure VNets, Virtual Network Peering!!

Per Microsoft’s online documentation, we have the options for virtual network peering within the same region or we can opt for global network peering, where needed. Each option has a different rate for inbound and outbound data transfers based on the region where your VNets are deployed. There are many benefits to peering for connecting our virtual networks, such as low latency, high bandwidth, and private connectivity between our resources in different virtual networks.

The following steps were taken to allow me to implement VNet Peering:
<ul>
  <li> Created two virtual networks </li>
  <li> Deployed a virtual machine (VM) into each virtual network </li>
  <li> Connected two virtual networks with a virtual network peering </li>
  <li> Tested communication between the VMs </li>
  <li> Deploying the Infrastructure (Steps 1–2) </li>
</ul>

I accomplished steps 1–2 by using a PowerShell script to quickly deploy my network infrastructure. In this deployment, we have two virtual networks, eus-vnet and wus-vnet, each deployed to different Azure Regions (East US and West US 3). We also have two virtual machines (eus-prod-server and wus-prod-server) both with Linux Ubuntu as the OS image. A public IP address was configured for the East US server to allow me to connect to it over the public Internet. A public IP address is a requirement in order to allow any Azure resource to receive inbound communication from the Internet. Both servers have private IP addresses that were assigned by Azure, taken from the address space of the virtual network subnets where the VMs were deployed to.


Network infrastructure deployed using a PowerShell script

```bash
$RGName = "ContosoResourceGroup"
   
New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateFile ManufacturingVMazuredeploy.json -TemplateParameterFile ManufacturingVMazuredeploy.parameters.json
```
![image](https://github.com/user-attachments/assets/98bff8eb-96d1-49b7-a3c8-d0f2d6d5e88b)

![image](https://github.com/user-attachments/assets/6928379e-700c-4588-9ff2-88a1c2f5e400)

Two virtual machines deployed to two different virtual networks

![image](https://github.com/user-attachments/assets/469d1724-c873-4028-b098-0906bbf7b514)


![image](https://github.com/user-attachments/assets/c8e80aa2-debe-44ff-9d23-7b64df89750f)


![image](https://github.com/user-attachments/assets/f3d6c238-d187-4a27-804c-08cd3761fda2)




![image](https://github.com/user-attachments/assets/ae1790e8-7aad-4ea6-86b6-8c2ffef334d6)


![image](https://github.com/user-attachments/assets/df241d4e-f2c0-4b0f-bd84-8b931f57ebb8)


![image](https://github.com/user-attachments/assets/16940963-e667-403d-831c-5e6bceb967e0)

![image](https://github.com/user-attachments/assets/5752b51d-797f-4406-bc8c-62956e95bd83)

![image](https://github.com/user-attachments/assets/14c2c8bb-c5ca-4ccf-97fc-b69b44cb9f08)

## Task 3: Test the connection between the VMs


![image](https://github.com/user-attachments/assets/e0940f1f-a10c-4657-bdf2-9f69d48cfe48)

![image](https://github.com/user-attachments/assets/5710b426-8183-48b0-8e75-eb5f79970651)

![image](https://github.com/user-attachments/assets/e3862adf-1c78-48b9-8e19-4f4854716503)

![image](https://github.com/user-attachments/assets/c6162b40-75b0-40f1-af6c-b8555f327bcc)


## Task 4: Create VNet peerings between CoreServicesVnet and ManufacturingVnet

![image](https://github.com/user-attachments/assets/991dddec-e783-4569-b028-a737245032fb)

![image](https://github.com/user-attachments/assets/b10919ae-917d-4fca-8213-03fc16d9ce5b)


![image](https://github.com/user-attachments/assets/6e661411-66f4-4e5a-9097-3ed88ad8c174)


![image](https://github.com/user-attachments/assets/f3067579-ddc7-4df9-84e2-0a8347e907c5)


![image](https://github.com/user-attachments/assets/6bd7465c-8399-4d83-bc1a-760d19a4a109)

![image](https://github.com/user-attachments/assets/49367e61-bf73-4076-b7ac-d2557c455003)

![image](https://github.com/user-attachments/assets/bb149d27-ff7a-4196-9d6c-f0f146f834d5)


![image](https://github.com/user-attachments/assets/4b98f300-87f8-4c9b-9abe-2529591cb24d)


![image](https://github.com/user-attachments/assets/a927dce8-aff7-4d2c-a11b-1195f6032e47)


![image](https://github.com/user-attachments/assets/987ec0a1-46ec-4632-be5b-28ac8c1cb2c2)

![image](https://github.com/user-attachments/assets/ceb7602e-450e-4135-b63d-df608cb98614)


![image](https://github.com/user-attachments/assets/dd5b075f-6df7-4f52-bc38-e9d8e129595e)

![image](https://github.com/user-attachments/assets/6e0ce6f1-c1c3-491f-95c3-e01a41975c36)

![image](https://github.com/user-attachments/assets/080d3c42-e147-4f78-a5b0-ce6a930778f3)

![image](https://github.com/user-attachments/assets/f01bde7e-d75f-4646-8756-1d0cfee43144)

![image](https://github.com/user-attachments/assets/eed86abb-19ba-47bd-ac90-142f584eb750)











