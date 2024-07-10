# File System Security Assessment: Detecting Unauthorized Access and Modifications

## Introduction
File system security is essential for ensuring that sensitive data is protected from unauthorized access and modifications. This project will guide you through a file system security assessment, focusing on identifying unauthorized access and changes to files. You will use various tools to monitor, analyze, and secure the file system.

## Pre-requisites
- Basic understanding of file system concepts (permissions, file types, etc.)
- Familiarity with the Linux command line
- A computer with a Linux operating system (preferably Ubuntu)
- Internet connection to download necessary tools

## Lab Setup and Tools
- **Lab Environment**: A single Linux machine with sudo access.
- **Tools**:
  - Auditd
  - Tripwire
  - AIDE (Advanced Intrusion Detection Environment)
  - OSSEC
  - Chkrootkit

## Exercises

### Exercise 1: Monitoring File Access with Auditd
**Objective**: Use Auditd to monitor and log file access events.

**Steps**:
1. **Install Auditd**:
    ```sh
    sudo apt-get update
    sudo apt-get install auditd
    ```

2. **Configure Audit Rules**:
    ```sh
    sudo auditctl -w /etc/passwd -p wa -k passwd_changes
    ```
   - This command sets up monitoring for write and attribute change access to `/etc/passwd`.

3. **View Audit Logs**:
    ```sh
    sudo ausearch -k passwd_changes
    ```

**Expected Output**:
- Log entries showing access events for the monitored file.

### Exercise 2: File Integrity Monitoring with Tripwire
**Objective**: Use Tripwire to detect unauthorized changes to files.

**Steps**:
1. **Install Tripwire**:
    ```sh
    sudo apt-get install tripwire
    ```

2. **Initialize Tripwire Database**:
    ```sh
    sudo tripwire --init
    ```

3. **Run a File Integrity Check**:
    ```sh
    sudo tripwire --check
    ```

**Expected Output**:
- Report detailing any changes or modifications to the monitored files.

### Exercise 3: System Integrity Check with AIDE
**Objective**: Use AIDE to perform a system integrity check.

**Steps**:
1. **Install AIDE**:
    ```sh
    sudo apt-get install aide
    ```

2. **Initialize AIDE Database**:
    ```sh
    sudo aideinit
    ```

3. **Run an Integrity Check**:
    ```sh
    sudo aide --check
    ```

**Expected Output**:
- Report highlighting any differences between the current file system state and the baseline.

### Exercise 4: Host-Based Intrusion Detection with OSSEC
**Objective**: Use OSSEC to monitor the system for suspicious activity.

**Steps**:
1. **Install OSSEC**:
    ```sh
    wget -q -O - https://updates.atomicorp.com/installers/atomic | sudo bash
    sudo yum install ossec-hids ossec-hids-server
    ```

2. **Configure OSSEC**:
    - Edit `/var/ossec/etc/ossec.conf` to define what should be monitored.

3. **Start OSSEC**:
    ```sh
    sudo systemctl start ossec
    ```

4. **View Alerts**:
    ```sh
    sudo tail -f /var/ossec/logs/alerts/alerts.log
    ```

**Expected Output**:
- Log entries showing detected suspicious activity.

### Exercise 5: Rootkit Detection with Chkrootkit
**Objective**: Use Chkrootkit to detect rootkits on the system.

**Steps**:
1. **Install Chkrootkit**:
    ```sh
    sudo apt-get install chkrootkit
    ```

2. **Run Chkrootkit**:
    ```sh
    sudo chkrootkit
    ```

**Expected Output**:
- Report indicating whether any rootkits were found on the system.

## Conclusion
By completing these exercises, you have learned how to monitor and assess file system security to detect unauthorized access and modifications. These skills are essential for maintaining the integrity and confidentiality of sensitive data in your system.
