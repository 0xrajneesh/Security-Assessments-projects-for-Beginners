# User Account Security Assessment: Evaluating User Permissions and Activity Logs

## Introduction
User account security is critical for preventing unauthorized access and ensuring that users have appropriate permissions. This project will guide you through a user account security assessment, focusing on evaluating user permissions and analyzing user activity logs. You will use various tools to audit, analyze, and secure user accounts.

## Pre-requisites
- Basic understanding of user account concepts (usernames, groups, permissions, etc.)
- Familiarity with the Linux command line
- A computer with a Linux operating system (preferably Ubuntu)
- Internet connection to download necessary tools

## Lab Setup and Tools
- **Lab Environment**: A single Linux machine with sudo access.
- **Tools**:
  - PAM (Pluggable Authentication Modules)
  - chkpasswd
  - sudo
  - usermod
  - faillog

## Exercises

### Exercise 1: Auditing User Accounts with PAM
**Objective**: Use PAM to audit user accounts and log authentication attempts.

**Steps**:
1. **Install PAM**:
    ```sh
    sudo apt-get update
    sudo apt-get install libpam0g-dev
    ```

2. **Configure PAM**:
    - Edit `/etc/pam.d/common-auth` to add the following line:
        ```sh
        auth required pam_tally2.so onerr=fail audit silent deny=5 unlock_time=900
        ```
      - This configuration will lock a user account for 15 minutes after 5 failed login attempts.

3. **View PAM Logs**:
    ```sh
    sudo tail -f /var/log/auth.log
    ```

**Expected Output**:
- Authentication logs showing login attempts and account locks.

### Exercise 2: Checking Password Strength with chkpasswd
**Objective**: Use chkpasswd to check the strength of user passwords.

**Steps**:
1. **Install chkpasswd**:
    ```sh
    sudo apt-get install chkpasswd
    ```

2. **Check Password Strength**:
    ```sh
    sudo chkpasswd
    ```

3. **Review Password Policies**:
    - Ensure that the password policies meet the organization’s security standards (minimum length, complexity, etc.).

**Expected Output**:
- Report detailing the strength of user passwords and compliance with password policies.

### Exercise 3: Auditing Sudo Permissions with sudo
**Objective**: Use sudo to audit user permissions and ensure appropriate access controls.

**Steps**:
1. **List Sudoers**:
    ```sh
    sudo cat /etc/sudoers
    sudo ls /etc/sudoers.d/
    ```

2. **Check User Permissions**:
    ```sh
    sudo -l -U username
    ```
   - Replace `username` with the user you want to audit.

3. **Review and Adjust Permissions**:
    - Edit `/etc/sudoers` or files in `/etc/sudoers.d/` to ensure users have the appropriate level of access.

**Expected Output**:
- List of users with sudo privileges and their specific permissions.

### Exercise 4: Modifying User Permissions with usermod
**Objective**: Use usermod to modify user permissions and group memberships.

**Steps**:
1. **Add User to Group**:
    ```sh
    sudo usermod -aG groupname username
    ```
   - Replace `groupname` with the group and `username` with the user you want to modify.

2. **Remove User from Group**:
    ```sh
    sudo gpasswd -d username groupname
    ```

3. **Verify Group Memberships**:
    ```sh
    groups username
    ```

**Expected Output**:
- Confirmation of changes to user group memberships.

### Exercise 5: Analyzing Failed Login Attempts with faillog
**Objective**: Use faillog to analyze failed login attempts and identify potential security issues.

**Steps**:
1. **View Failed Login Attempts**:
    ```sh
    sudo faillog
    ```

2. **Reset Failed Login Count for a User**:
    ```sh
    sudo faillog -r -u username
    ```
   - Replace `username` with the user whose failed login count you want to reset.

3. **Configure Login Failure Limits**:
    - Edit `/etc/login.defs` to set the maximum number of allowed failed login attempts:
        ```sh
        FAILLOG_ENAB yes
        FAIL_DELAY 4
        LOGIN_RETRIES 5
        ```

**Expected Output**:
- List of failed login attempts and confirmation of any resets or configuration changes.

## Conclusion
By completing these exercises, you have learned how to evaluate user permissions and analyze user activity logs to ensure user account security. These skills are essential for preventing unauthorized access and maintaining the integrity of user accounts in your system.
