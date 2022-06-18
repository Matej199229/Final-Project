# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Hypervisor machine
  - **Operating System**:Windows 10
  - **Purpose**:Hypervisor machine that hosts the rest of the VMs on virtual network below
  - **IP Address**:192.168.1.1
- ELK Server
  - **Operating System**:Linux
  - **Purpose**:server that holds Kibana dashboards for monitoring
  - **IP Address**:192.168.1.100
- Capstone
**Operating System**:Linux
  - **Purpose**:Vulnerable VM that we exploited in Project 2. Filebeat and Metricbeat are installed and will forward logs to the ELK machine as well.
  - **IP Address**:192.168.1.105
  Target 1
**Operating System**:Linux
  - **Purpose**:Target 1 VM with a vulnerable WordPress server to exploit 
  - **IP Address**:192.168.1.110
  Target 2
**Operating System**:Linux
  - **Purpose**:Target 2 vulnerable VM to exploit.
  - **IP Address**:192.168.1.115
  Kali Attack machine
**Operating System**:Kali Linux
  - **Purpose**:Attacker machine used to exploit Target 1 and Target 2 VMs
  - **IP Address**:192.168.1.90
  

### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors Alert

Excessive HTTP Errors Alert is implemented as follows:
  - **Metric**: WHEN count() GROUPED OVER top 5 'http.response.status_code'
  - **Threshold**: IS ABOVE 400 FOR THE LAST 5 minutes
  - **Vulnerability Mitigated**: brute forcing attacks/enumeration
  - **Reliability**: Generally this alert should be highly reliable as it excludes all successful response codes and focuses on all of the 400 and 500 error codes ones that are of more concern.

#### HTTP Request Size Monitor Alert
HTTP Request Size Monitor Alert is implemented as follows:
  - **Metric**: WHEN sum() of http.request.bytes OVER all documents
  - **Threshold**: IS ABOVE 3500 FOR THE LAST 1 minute
  - **Vulnerability Mitigated**: malicious payloads and code injection
  - **Reliability**: Low/Medium - Assumes that all bad files must be of a large byte size and may not detect smaller ones. In addition, 3500 is also a small byte size and may result in multiple false positives

#### CPU Usage Monitor Alert
CPU Usage Monitor Alert is implemented as follows:
  - **Metric**: WHEN max() OF system.process.cpu.total.pct OVER all documents
  - **Threshold**: IS ABOVE 0.5 FOR THE LAST 5 minutes
  - **Vulnerability Mitigated**: malware, DDoS
  - **Reliability**: Highly reliable. Even if the alerts did not capture malicious program, it can help determine where to improve on CPU performance


### Suggestions for Going Further (Optional)
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 2
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 3
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
