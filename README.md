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
2. Navigate to the Virtual Machines service.
3. Click on "Create" to begin the VM creation process.
4. Select an appropriate operating system image (e.g., Windows or Linux).
5. Configure the VM settings, including size, networking, and authentication.
6. Ensure to enable Remote Desktop Protocol (RDP) or Secure Shell (SSH) access for management purposes.
7. Optionally, customize the VM with additional software or configurations to introduce specific vulnerabilities.

### Step 2: Harden Security (Optional)

**Purpose:** Implement basic security measures to protect the vulnerable VMs.

1. Install security updates and patches on the VMs.
2. Configure firewalls to restrict unnecessary network traffic.
3. Disable unnecessary services and remove unused software.
4. Implement strong authentication mechanisms, such as complex passwords or multi-factor authentication.
5. Regularly monitor and audit the VMs for suspicious activities.

### Step 3: Test and Exploit Vulnerabilities

**Purpose:** Identify and exploit vulnerabilities within the VM environment.

1. Use vulnerability scanning tools like Nessus or OpenVAS to scan the VMs for known vulnerabilities.
2. Exploit identified vulnerabilities using penetration testing tools like Metasploit or Burp Suite.
3. Document the vulnerabilities discovered and potential impacts.
4. Develop and implement strategies to mitigate the identified vulnerabilities, such as applying patches, configuring security settings, or updating software versions.

## Conclusion

Setting up vulnerable VMs in Azure provides an invaluable learning experience for understanding common security issues and practicing cybersecurity skills. By actively engaging with vulnerable environments, users can enhance their knowledge of security concepts, threat detection, and mitigation strategies, ultimately improving their ability to protect against real-world cyber threats.

![Azure Portal](image_url_1)

![VM Configuration](image_url_2)
