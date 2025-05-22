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

**Public IP Address of the VM**
The public IP address of my VM is: 172.177.233.83
**Screenshot of Web Browser Successfully Accessing the Website:**
![created_resource](images/week8-task4-accessing_web.png)
**Network Security Rules Allowing Access to the VM**
There are two network security rules that allow access to my VM:
- **Port 22 (SSH)(default-allow-ssh)**: This rule allows the Secure Shell (SSH) protocol, which I used to remotely log in to the VM and manage it (e.g., to edit the webpage).
- **Port 80 (HTTP)(AllowAnyHTTPInbound)**: This rule allows Hypertext Transfer Protocol (HTTP), which enables web traffic so that I can access the website hosted on the VM through a browser.

## Task 5: Compare Cloud vs On-premise Costs

## Task 6. Create a Storage Blob in Azure

**Screenshot of One Image and Its Full URL**
I uploaded an image to the `ishfaque` container, which has Blob-level anonymous access. Below is the screenshot and the URL to access the image:

![an_image](images/week8-task6_image.png)
- **Full URL**: `https://cloudshell51579565.blob.core.windows.net/ishfaque/TSV-Building-21_029-2-1536x983.webp`

**Screenshot of Azure Portal Resources Showing the Container(s)**
In the Azure Portal, I created a container in the storage account `cloudshell51579565`. Here are the details:
  - **Container: ishfaque**
    - **Last Modified**: 5/22/2025, 10:31:56 PM
    - **Anonymous Access Level**: Blob (anonymous read access for blobs only)
    - **Lease State**: Available
![container](images/week8-task6_container.png)

## Task 7. Create a Resource Lock
**Difference Between Locks:**
- **Read-Only Lock**: When I applied a Read-Only Lock to one of my resources (like a storage account I created earlier), I noticed that I couldn’t make any changes to it. For example, I tried to update the access level of a container, but the portal blocked the action and showed an error saying the resource was locked. However, I could still view the resource details and access the data inside it. This lock is really useful when I want to make sure no one accidentally changes a resource, especially if it’s being used in a live project or needs to stay the same for testing.
- **Delete Lock**: Next, I applied a Delete Lock to another resource. With this lock in place, I couldn’t delete the VM even when I tried to remove it through the Azure Portal—it gave me an error saying deletion was not allowed due to the lock. But I was still able to modify the VM, like changing its size or adding a new network rule. This lock is great for protecting important resources from being accidentally deleted, while still letting me make updates as needed during the lab.
