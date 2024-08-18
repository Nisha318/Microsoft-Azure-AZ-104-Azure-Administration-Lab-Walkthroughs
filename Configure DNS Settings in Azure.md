#  Configure DNS Settings in Azure

## Task 1: Create a private DNS Zone

![image](https://github.com/user-attachments/assets/6797e6b1-3066-4e4b-ae94-df5b4ff6d5cc)

![image](https://github.com/user-attachments/assets/e653a34e-2d98-4cca-a641-1230450fcae1)


## Task 2: Link subnet for auto registration

![image](https://github.com/user-attachments/assets/457a17ca-da85-44fb-85c1-8466d29b6d65)

![image](https://github.com/user-attachments/assets/f226d8d7-f872-4d88-96fa-ca48aa697c0f)

![image](https://github.com/user-attachments/assets/390729a1-8639-4361-be4d-1ae5638ec667)


![image](https://github.com/user-attachments/assets/6daff9f8-a954-4722-af43-e494a01b4246)




## Task 3: Create Virtual Machines to test the configuration


![image](https://github.com/user-attachments/assets/7962a9f1-a2b7-48d3-8c5e-5b8dc2d921c1)

![image](https://github.com/user-attachments/assets/e6c399e1-363f-408d-bce7-0108f43b192e)



![image](https://github.com/user-attachments/assets/b662c9b0-30bd-4229-95c3-bf947d3105dc)


```bash
$RGName = "ContosoResourceGroup"
   
New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateFile azuredeploy.json -TemplateParameterFile azuredeploy.parameters.json
```


![image](https://github.com/user-attachments/assets/d5e93f1b-78cc-4c99-b902-d79db18c637b)

![image](https://github.com/user-attachments/assets/57e4dfc3-9acd-45b9-89cb-727bf16a806b)


![image](https://github.com/user-attachments/assets/a4597ef7-54a6-4e24-b036-ce5944bfbff0)



## Task 4: Verify records are present in the DNS zone

![image](https://github.com/user-attachments/assets/cd840f00-c844-4b40-b998-c61c657f317c)

![image](https://github.com/user-attachments/assets/e613562d-8437-459f-b5c1-904143b0fc12)



## Connect to the Test VMs using RDP


![image](https://github.com/user-attachments/assets/faad6e23-dcda-49b6-a09c-96b4e8a146fb)



![image](https://github.com/user-attachments/assets/35245806-62cb-47bf-bc68-df454cce4f36)



![image](https://github.com/user-attachments/assets/fa3ed08f-0f63-48d4-af61-692a24f4af80)


![image](https://github.com/user-attachments/assets/8f1eac22-06a0-4565-8f18-1f0098d29d5b)


![image](https://github.com/user-attachments/assets/e0e94b82-148d-4e50-b1a7-dff62627ae6d)


![image](https://github.com/user-attachments/assets/9bd411d4-805e-4ca1-bdd6-8737ed467629)


![image](https://github.com/user-attachments/assets/96a8b796-770b-4e2f-a1fd-cca4ebb8c3cb)



![image](https://github.com/user-attachments/assets/1cfe3aa8-bcec-4c0a-ac92-7df59e2e419a)


![image](https://github.com/user-attachments/assets/72afdfe5-78f9-4922-bf9e-a502067676d7)


![image](https://github.com/user-attachments/assets/718cfa4d-4984-4c09-bfdf-03acfdc6fa07)


![image](https://github.com/user-attachments/assets/e4400863-8c16-4cb5-8d46-98ada092ad6e)



![image](https://github.com/user-attachments/assets/b1821b3f-743b-4bc3-bc68-ed7c93100ad8)


![image](https://github.com/user-attachments/assets/0f054809-822c-4d51-bc55-6e06ab0620e7)


![image](https://github.com/user-attachments/assets/f5c99b8e-8f1d-4404-a75d-27c1da51e62c)

