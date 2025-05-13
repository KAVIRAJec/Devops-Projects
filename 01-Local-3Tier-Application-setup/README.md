# 3-Tier Application Setup with Vagrant and VirtualBox

## Project Overview
This project demonstrates the setup of a 3-tier application architecture using VirtualBox for virtualization and Vagrant for provisioning. The 3-tier architecture includes:
1. **Database Layer**: MySQL
2. **Caching Layer**: Memcached
3. **Application Layer**: Tomcat server
4. **Message Broker**: RabbitMQ
5. **Web Server**: Nginx

The project includes both **manual provisioning** and **automated provisioning** using shell scripts to configure the virtual machines (VMs) for each layer.

---

## What is Virtualization?
Virtualization is the process of creating virtual instances of computing resources, such as servers, storage, and networks, on a single physical machine. It allows multiple virtual machines (VMs) to run on a single host, each with its own operating system and resources.

### What is a Virtual Machine (VM)?
A virtual machine is a software-based emulation of a physical computer. It runs an operating system and applications just like a physical machine but is isolated from the host system.

In this project, VirtualBox is used as the virtualization platform to create and manage VMs.

---

## Tools and Technologies Used
### Virtualization
- **Oracle VM VirtualBox**: A free and open-source virtualization tool to create and manage VMs.

### Provisioning
- **Vagrant**: A tool for managing virtual machine environments in a consistent and repeatable manner.
  - **Manual Provisioning**: VMs are configured manually using Vagrantfiles.
  - **Automated Provisioning**: Shell scripts are used to automate the setup of each VM.

### Software Stack
- **Database**: MySQL
- **Caching**: Memcached
- **Application Server**: Tomcat
- **Message Broker**: RabbitMQ
- **Web Server**: Nginx

---

## How It Works
### Manual Provisioning
The `Manual_provisioning_Vagrant` folder contains a `Vagrantfile` that defines the configuration for each VM. You can manually set up the VMs by running `vagrant up` and configuring each VM individually using `VprofileProjectSetupWindowsAndMacIntel.pdf` as a reference.

### Automated Provisioning
The `Automated_provisioning_Vagrant` folder contains:
- A `Vagrantfile` to define the VMs.
- Shell scripts (`*.sh`) to automate the setup of each VM:
  - `backend.sh`: Configures the backend services.
  - `memcache.sh`: Sets up Memcached.
  - `mysql.sh`: Installs and configures MySQL.
  - `nginx.sh`: Configures the Nginx web server.
  - `rabbitmq.sh`: Sets up RabbitMQ.
  - `tomcat.sh` and `tomcat_ubuntu.sh`: Install and configure the Tomcat server.

To automate the provisioning:
1. Navigate to the `Automated_provisioning_Vagrant` folder.
2. Run `vagrant up`. Vagrant will create and configure the VMs using the provided shell scripts.

---

## VM Configuration
The project creates multiple VMs, each serving a specific role in the 3-tier architecture:
1. **Database VM**: Runs MySQL.
2. **Caching VM**: Runs Memcached.
3. **Application VM**: Runs the Tomcat server.
4. **Message Broker VM**: Runs RabbitMQ.
5. **Web Server VM**: Runs Nginx.

---

## Prerequisites
1. Install [Oracle VM VirtualBox](https://www.virtualbox.org/).
2. Install [Vagrant](https://www.vagrantup.com/).
3. Install a terminal emulator (e.g., Git Bash for Windows).

---

## Steps to Run the Project
1. Clone the repository or download the project files.
2. Choose between manual or automated provisioning:
   - For manual provisioning, navigate to the `Manual_provisioning_Vagrant` folder.
   - For automated provisioning, navigate to the `Automated_provisioning_Vagrant` folder.
3. Run `vagrant up` to create and provision the VMs.
4. Access the services on the respective VMs.

---

## Architecture Diagram
Refer to the architecture diagrams in the `architecturediagrams` folder for a visual representation of the setup.

---

## Additional Notes
- Ensure that your system has sufficient resources (CPU, RAM, and disk space) to run multiple VMs simultaneously.
- The automated provisioning scripts are designed for Ubuntu-based VMs. Modify them if you use a different OS.

---
