![banner](honeypot.png)
# Setting Up Vulnerable VMs in Azure

This repository contains instructions for setting up vulnerable virtual machines (VMs) in Azure. These VMs are intentionally configured with vulnerabilities for educational and testing purposes, allowing users to learn about common security issues and practice vulnerability assessment and mitigation techniques.

## Prerequisites

Before getting started, ensure you have the following:

- An Azure account ([Sign up here](https://azure.microsoft.com/en-us/free))
  -   If you're a student, you can use the [Azure for Students](https://azure.microsoft.com/en-gb/free/students) program.
  
- Basic knowledge of Azure services and virtual machines

## Setup Instructions

### Step 1: Create Virtual Machines

**Purpose:** Deploy virtual machines with intentionally vulnerable configurations.

1. Log in to the Azure portal.
   - I would recommend bookmarking the url for the Azure portal with the browser of your choice for ease of accessibility.

2. Navigate to the Create a resource service.   
3. Under "Virtual Machine" click on "Create" to begin the VM creation process.
   
    ![VM-1](Create-VM.png)
   
5. Create a new resource group, with is a logical grouping of resources, where the VM will be placed.
     - Also give your VM a name, choose which region this VM will be hosted, availibility zone, and security type
     - For this example, I will be using a Windows 10 Image with x64 VM Architecture

        ![VM-2](Create-VM-1.png)
   
6. Configure Administrator account for your VM.
     - The username and password you establish will be your credentials to access your VM.
     - Allow the Public Inbound Ports to stay at the default setting of "Allow Selected Ports" as RDP (Remote Desktop Protocol) is how we will access the VM.
     - Tick the Licensing checkbox, and press Next until you come to the Network portion of the VM creation steps.

       ![VM-2](Create-VM-2.png)
       
7. Configure the NIC Network Security Group.
    - Here we will be creating a new Security Group that will essentially allow us access to modify the inbound rules of your VM.
    - Change the NIC Network Security Group to Advanced, and it will populate a new field.
    - With this "Configure Network Security" Group Field, click "Create New" underneath the dropdown.

      ![VM-2](Create-VM-Network-1.png)

8. Remove Default Inbound rule.
     - Once in this menu, you will see the default inbound rule, remove it by clicking the trash can icon to the right.
     - Then, click the "+ Add Inbound Rule" to create our new vulnerable inbound rule.

        ![VM-2](Create-VM-Network-2.png)
  
9. Create a Vulnerable Inbound Rule
     - IMPORTANT: This is for purposely creating a vulnerable resource and you would never do this otherwise.
     - Edit the Destination Port Ranges to be an asterisk "*", meaning allow any and all ports to be accessed.
     - Allow any protocol, and allow action
     - Change the Priority to 100
           - In Azure, the priority is used to determine the order in which the rules are processed. The lower the number, the higher the priority, and the earlier the rule is processed.
     - Lastly, add a name for this rule. In this case I put "DANGER_ANY_IN" to reflect this rule is very vulnerable as it can be accessed by anyone via any port.
     - Click the "Add" Button to add it to your inboud rules for your VM.
  
       ![VM-2](Create-VM-Network-3.png)
  
       ![VM-2](Create-VM-Network-4.png)
  
10. Create the VM
    - Once you've added the inbound rule, click the Create button at the bottom left.
    - This may take some time for Azure to "spin up" your VM, but once it is completed you'll see it with a status of "Running". 


### Step 2: RDP Onto The VM

**Purpose:** To Access the VM remotely.

1. Once the VM is created and running, open the Azure portal.
2. Navigate to the list of virtual machines.
3. Click on the VM you created.
4. Under the "Overview" section, find the "Public IP Address" field.
     - This will be the IP Address we will use, along with the credentials made during the creation of the VM, to remotely access the VM.

      ![VM-2](Public_IP.png)
   
5. Copy this IP Address.
6a. For Windows Users, search for "RDP" in the bottom left Search Bar.
    - Once this interface opens, it will prompt for a Computer and Username field
    - You'll paste the VM's Public IP Address in the Computer field
    - You'll use the username crediential that you established when creating the Administrator Account for your VM
    - Click "Connect" at the bottom left
    - It'll prompt you for a Password, this is the same password that you've created when establishing the Administrator Account for your VM
    - It'll trigger a popup stating that "Remote computer cannot be verified" just click the Yes button at the bottom left
    - If you followed these steps, then you should be Remoting into your VM right now.
      
     ![VM-2](RDP_IMAGE.png)
   
6b. For Mac Users, go to the App Store and download "Microsoft Remote Desktop".
  - Once installed, open it.
  - Click the "Add PC" Button
  - For the PC Name, paste the Public IP Address
  - Click the drop down for User Account
      - Create a new user account using the username and password you created when establishing the Administrator Account for your VM
  - Check the "Connect to an admin session" box
  - Click the "Add" Button
  - Now click the elipses > Connect
  - It will prompt stating that  "Remote computer cannot be verified" just click the Yes button
  - If you followed these steps, then you should be Remoting into your VM right now.

6c. You will now have remote access to the VM's desktop environment, allowing you to interact with it as if you were physically present.

   ![VM-2](VM-Snapshot.png)

### Step 3: Test Ping/Disable Firewalls

**Purpose:** Validate network connectivity and adjust firewall settings if necessary.

1. Open a command prompt or terminal on your local machine.
2. Ping the public IP address of the Azure VM to test network connectivity.
   - If you receive a response, the VM is reachable from your local machine.
   - If you encounter "Request timed out" messages, it may indicate firewall restrictions. Proceed to the next step.
     
     ![VM-2](Ping-Before-Firewall-Disable.png)
     
3. Disable the firewall on the Azure VM temporarily for testing purposes:
   - IMPORTANT: This is for purposely creating a vulnerable resource and you would never do this otherwise.
   - In the VM you are currenty remotely connected to, search "wf.msc"
   - This will bring up the Windows Defender Firewall Menu

     ![VM-2](Firewall-Menu-1.png)
     
   - From here, click the "Windows Defender Firewall Properties"
   - Now, disable the Firewalls for the Domain Profile, Private Profile, and Public Profile

     ![VM-2](Firewall-Disable-1.png)
     
     ![VM-2](Firewall-Disable-2.png)
     
     ![VM-2](Firewall-Disable-3.png)

   - Once they are all changed to Off, click Apply followed by Okay.


  4. Back on your host machine, open up the terminal and run the ping command once again
     - You should start receiving responses from the Virtual Machine

        ![VM-2](Ping-After-Firewall-Disable.png)


These steps ensure that you can establish remote desktop connections to the VM and troubleshoot any network connectivity issues by testing ping and adjusting firewall settings accordingly.

## Conclusion

Setting up vulnerable VMs in Azure provides an invaluable learning experience for understanding common security issues and practicing cybersecurity skills. By actively engaging with vulnerable environments, users can enhance their knowledge of security concepts, threat detection, and mitigation strategies, ultimately improving their ability to protect against real-world cyber threats.
