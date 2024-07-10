# System Log Assessment: Analyzing Logs for Potential Security Incidents

## Introduction
System logs are vital for tracking system activities, diagnosing issues, and identifying potential security incidents. This project will guide you through a system log assessment, focusing on analyzing logs to detect suspicious activities. You will use various tools to collect, analyze, and interpret log data.

## Pre-requisites
- Basic understanding of system logging concepts (log files, log levels, etc.)
- Familiarity with the Linux command line
- A computer with a Linux operating system (preferably Ubuntu)
- Internet connection to download necessary tools

## Lab Setup and Tools
- **Lab Environment**: A single Linux machine with sudo access.
- **Tools**:
  - Rsyslog
  - Logwatch
  - Logrotate
  - Splunk
  - ELK Stack (Elasticsearch, Logstash, Kibana)

## Exercises

### Exercise 1: Configuring Centralized Logging with Rsyslog
**Objective**: Configure Rsyslog for centralized logging and ensure logs are collected in a centralized location.

**Steps**:
1. **Install Rsyslog**:
    ```sh
    sudo apt-get update
    sudo apt-get install rsyslog
    ```

2. **Configure Rsyslog**:
    - Edit `/etc/rsyslog.conf` to enable centralized logging.
    - Add the following lines to forward logs to a remote log server:
        ```sh
        *.* @192.168.1.100:514
        ```
      - Replace `192.168.1.100` with the IP address of your remote log server.

3. **Restart Rsyslog**:
    ```sh
    sudo systemctl restart rsyslog
    ```

**Expected Output**:
- Logs should be forwarded to the specified remote log server.

### Exercise 2: Log Analysis with Logwatch
**Objective**: Use Logwatch to generate daily reports from system logs.

**Steps**:
1. **Install Logwatch**:
    ```sh
    sudo apt-get install logwatch
    ```

2. **Generate a Log Report**:
    ```sh
    sudo logwatch --detail high --logfile /var/log/syslog --range today --service all --print
    ```

**Expected Output**:
- Detailed log report summarizing system activities for the day.

### Exercise 3: Log Rotation with Logrotate
**Objective**: Use Logrotate to manage and rotate log files to prevent them from growing indefinitely.

**Steps**:
1. **Configure Logrotate**:
    - Edit or create a configuration file for your logs, e.g., `/etc/logrotate.d/custom_logs`:
        ```sh
        /var/log/custom_log {
            daily
            rotate 7
            compress
            missingok
            notifempty
            create 0640 root utmp
        }
        ```

2. **Test Logrotate Configuration**:
    ```sh
    sudo logrotate -d /etc/logrotate.d/custom_logs
    ```

**Expected Output**:
- Log files should be rotated daily, with the last 7 days retained, and compressed to save space.

### Exercise 4: Real-time Log Monitoring with Splunk
**Objective**: Use Splunk to collect, index, and monitor system logs in real-time.

**Steps**:
1. **Install Splunk**:
    ```sh
    wget -O splunk-8.0.5-152fb4b2bb96-Linux-x86_64.deb "https://www.splunk.com/page/download_track?file=8.0.5/linux/splunk-8.0.5-152fb4b2bb96-Linux-x86_64.deb"
    sudo dpkg -i splunk-8.0.5-152fb4b2bb96-Linux-x86_64.deb
    ```

2. **Start Splunk**:
    ```sh
    sudo /opt/splunk/bin/splunk start --accept-license
    sudo /opt/splunk/bin/splunk enable boot-start
    ```

3. **Add Data Sources**:
    - Access Splunk web interface at `http://localhost:8000`.
    - Add `/var/log` directory as a data source to monitor system logs.

**Expected Output**:
- Real-time log monitoring dashboard in Splunk showing collected logs.

### Exercise 5: Visualizing Log Data with the ELK Stack
**Objective**: Use the ELK Stack (Elasticsearch, Logstash, Kibana) to collect, process, and visualize log data.

**Steps**:
1. **Install Elasticsearch**:
    ```sh
    sudo apt-get install elasticsearch
    sudo systemctl start elasticsearch
    sudo systemctl enable elasticsearch
    ```

2. **Install Logstash**:
    ```sh
    sudo apt-get install logstash
    ```

3. **Configure Logstash**:
    - Create a configuration file `/etc/logstash/conf.d/logstash.conf`:
        ```sh
        input {
          file {
            path => "/var/log/syslog"
            start_position => "beginning"
          }
        }
        output {
          elasticsearch {
            hosts => ["localhost:9200"]
            index => "syslog"
          }
        }
        ```

4. **Start Logstash**:
    ```sh
    sudo systemctl start logstash
    sudo systemctl enable logstash
    ```

5. **Install Kibana**:
    ```sh
    sudo apt-get install kibana
    sudo systemctl start kibana
    sudo systemctl enable kibana
    ```

6. **Access Kibana**:
    - Open a browser and navigate to `http://localhost:5601`.
    - Configure Kibana to use the `syslog` index and create visualizations.

**Expected Output**:
- Interactive dashboards in Kibana displaying log data from Elasticsearch.

## Conclusion
By completing these exercises, you have learned how to collect, analyze, and interpret system logs using various tools. These skills are essential for detecting and responding to potential security incidents in your system.
