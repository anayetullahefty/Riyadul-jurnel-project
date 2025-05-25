
## Task 2: Login to Microsoft Learn on Demand
Visited https://msle.learnondemand.net/, selected "Register with Training Key," and created a Skillable account using my @cqumail.com address. Then logged in with the Skillable account.
![login_microsoft_learn_on_demand](images/week8-task2_login_microsoft_learn_on_demand.png)

## Task 3: Create an Azure Resource
In this task, I created Azure Resources using the Azure portal by followed the provided instructions.

#### List of Resources:
- **my-VM-51382442 (Virtual Machine)**: This is the main compute resource, an Ubuntu VM, used to run applications and host services like a web server.
- **my-VM-51382442-ip (Public IP Address)**: Assigns a public IP to the VM, enabling external access to the VM, such as for SSH or web access.
- **my-VM-51382442-nsg (Network Security Group)**: Defines security rules to control inbound and outbound traffic to the VM, such as allowing SSH (port 22) and HTTP (port 80).
- **my-VM-51382442-vnet (Virtual Network)**: Provides an isolated network environment for the VM to communicate with other Azure resources securely.
- **my-vm-51382442625_z1 (Network Interface)**: Connects the VM to the virtual network, enabling network communication.
- **my-VM-51382442_OsDisk_1_b32a2286... (Disk)**: The operating system disk for the VM, storing the Ubuntu OS and related system files.

![list_of_resources](images/week8-task3_list_of_resources.png)

## Task 4: Create an Azure Virtual Machine and Allow Web Access
**Azure Commands:** To create a Linux VM and configure Nginx on the VM.
```
# To create a Linux VM
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
```
**Public IP Address:** 172.203.77.6

**Successfully accessing website with my name**:
![created_resource](images/week8-task4-accessing_web.png)
**Network Security Rules:**
- Port 22 (SSH):
  - Rule Name: default-allow-ssh
  - Description: Allows Secure Shell (SSH) access to the VM for remote administration.
- Port 80 (HTTP):
  - Rule Name: AllowAnyHTTPInbound
  - Description: Allows Hypertext Transfer Protocol (HTTP) access to serve web content.
  
## Task 5: Compare Cloud vs On-premise Costs

### Specifications and Costs Table

| **Type**           | **CPU**          | **GPU**         | **RAM** | **Storage** | **Upfront Cost (AUD)** | **1-Year Running Cost (AUD)** | **3-Year Running Cost (AUD)** |
|---------------------|------------------|-----------------|---------|-------------|-------------------------|-------------------------------|-------------------------------|
| Consumer Desktop PC | Intel Core i5-12400F | ZOTAC GeForce RTX 4060 8GB | 16GB DDR5 5600MHz | 1TB NVMe SSD | 1,349                   | 150 (electricity)             | 450 (electricity)             |
| Azure VM            | 4 vCPUs (D4 v5)  | N/A (GPU not specified) | 16GB    | 1TB SSD     | 0 (no upfront cost)     | 3,838.92 (monthly $319.91)    | 11,515.52 (monthly $319.91)    |

### Consumer PC Cost  
I found the desktop PC on [PC Case Gear](https://www.pccasegear.com/products/68710/pccg-banshee-4060-gaming-pc).

![Consumer PC Cost](images/week08-task5-consumarPC.png)

### Azure Pricing Calculator  
After exporting this price, I convert it to Australian dollars. 
Currency Conversion: 1 USD = 1.52 AUD (xe.com, May 2025).
Azure VM Pricing(3 Yeras): $210.47 USD/month × 12 × 3 = $7,576.92 USD × 1.52 = $11,515.52 AUD.
![Azure Pricing Calculator](images/week08-task5-azureCost.png)

### Trade-offs Discussion  
Now that the Azure VM meets the requirements, the comparison feels fairer. The desktop PC is still cheaper overall—AUD 1,349 over 1 year and AUD 1,1949 over 3 years, compared to the Azure VM’s AUD 3,838.92 and AUD 11,515.52. That’s a big cost difference, especially over 3 years, since the PC’s main expense is upfront, and electricity isn’t much. The PC also has a great GPU (RTX 4060 8GB), which is perfect for design work, while the Azure VM doesn’t include a GPU, so it’s not as good for those tasks. Both have 16GB RAM and similar CPU power (i5-12400F with 6 cores vs. 4 vCPUs), but the PC’s extra cores give it a slight edge for multitasking. The downside with the PC is that I’d need to handle maintenance—like fixing hardware or upgrading parts—which could add costs, and I’d have to manage security updates myself.

The Azure VM is more expensive, but it has some advantages. There’s no upfront cost, which is nice if I don’t have AUD 1,349 to spend right away. I can scale it up easily—like adding more CPU or storage—while upgrading the PC means buying new hardware. Azure takes care of maintenance, backups, and security updates, which saves me time, and I can access it from anywhere, unlike the PC, which stays at home. But the monthly cost adds up fast, and if I forget to turn it off, I’ll end up paying more. Also, slow internet could make it tricky to use, and without a GPU, it’s not great for graphics-heavy tasks.

For me, the desktop PC is the better choice because it’s way cheaper and has a GPU, which I’d use for gaming. The Azure VM makes sense if I need flexibility and don’t want to deal with hardware maintenance, but the cost difference makes the PC more practical for my needs.

## Task 6. Create a Storage Blob in Azure
**Screenshot of Image:** Displays one image uploaded to the created container.
![an_image](images/week8-task6_image.png)

**Screenshot of Azure Portal:** Shows the created container in the Azure Portal.
![container](images/week8-task6_container.png)

## Task 7. Create a Resource Lock
**Difference Between Locks:**
- **Read-Only Lock:** Blocks changes to a resource's configuration or properties (e.g., editing settings or resizing a VM), ensuring the resource remains as-is. Useful for protecting resource settings from accidental modifications.
- **Delete Lock:** Prevents a resource from being deleted, ensuring it remains in the Azure environment, but allows changes to its configuration or properties. Ideal for safeguarding critical resources from accidental removal.
