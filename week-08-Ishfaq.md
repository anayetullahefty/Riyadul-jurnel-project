## Task 2: Login to Microsoft Learn on Demand
![login_microsoft_learn_on_demand](images/week08-task2-login.png)

## Task 3: Create an Azure Resource
List the resources that were created and give a short explanation of what each resource is for: 
- **Resource Group (myRGKV-lod51575781)**  
  A container that holds related resources for an Azure solution, used to manage and organize resources efficiently.
- **Virtual Network (ishfaque-VN)**: Provides an isolated network for Azure resources, enabling secure communication between them.
- **Virtual Machine (my-VM-51575781)**: A compute resource that runs applications or services in the cloud, in this case, an Ubuntu-based VM.
- **Public IP Address (my-VM-51575781-ip)**: Assigns a public IP to the VM, allowing external access to the virtual machine over the internet.
- **Network Security Group (my-VM-51575781-nsg)**: Controls inbound and outbound traffic to network interfaces, ensuring security by defining access rules.
- **Network Interface (my-vm-51575781n176_z1)**: Connects the virtual machine to the virtual network, enabling network communication.
- **Disk (my-VM-51575781_OsDisk_1_2361b12719494d1b92e5bc44dd9f510)**: Provides persistent storage for the operating system and data of the virtual machine.
![list_of_resources](images/week8-task3_list_of_resources.png)

## Task 4: Create an Azure Virtual Machine and Allow Web Access
- **az Commands Used to Create the VM and Install Nginx**  
  Here are the commands I used to create the virtual machine and set up Nginx on it:  
  ```bash
  az vm create \
  --resource-group myRGKV-lod51383315 \
  --name my-VM-51383315 \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys

  # To configure Nginx on VM
  az vm extension set \
  --resource-group myRGKV-lod51383315 \
  --vm-name my-VM-51383315 \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --version 2.1 \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
