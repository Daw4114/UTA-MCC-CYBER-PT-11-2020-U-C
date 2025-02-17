# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Name of VM 1 Hyper V Host Manager
  - **Operating System**: Windows 10
  - **Purpose**: Contains the Vuln. machines & the attacking machine
  - **IP Address**: 192.168.1.1
- Name of VM 2 Kali
  - **Operating System**: Linux 5.4.0
  - **Purpose**: Used as attacking machine
  - **IP Address**: 192.168.1.90
  - - Name of VM 3 capstone
  - **Operating System**: Linux (Ubuntu 18.04)
  - **Purpose**: Used as a testing system for alerts
  - **IP Address**: 192.168.1.100
  - - Name of VM 4: ELK
  - **Operating System**: Linux (Ubuntu 18.04)
  - **Purpose**: Used for gathering info from victim machine using metricbeat, filebeat, and packetbeat
  - **IP Address**: 192.168.1.110
- - Name of VM 5 Target 1
  - **Operating System**: Linux 3.2 - 4.9
  - **Purpose**: The VM w/ WordPress as a vuln. server
  - **IP Address**: 192.168.1.110

### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110) & Target 2 (192.168.1.115)

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors
Alert 1 is implemented as follows:
  - **Metric**: Packetbeat: http.response.status_code > 400
  - **Threshold**: Grouped http response status codes above 400 every 5 minutes
  - When count() GROUPED OVER top5 'http.response.status_code' is above 400 for the last 5 minutes
  - **Vulnerability Mitigated**: Used IDS/IPS for attacks (IPS would block any suspicious IP's
  - Utilize Account Management to lock or request user accounts to change passwords every 60 days
  - filter & disable or close port 22
  - **Reliability**: Medium. This alert will not generate an excess amount of false positves identifying brute force attacks
  - 
#### CPU Usage Monitor
Alert 2 is implemented as follows:
  - **Metric**: Metricbeat: system.process.cpu.total.pct
  - **Threshold**: The total percentage is over 0.5% in 5 minutes
  - **Vulnerability Mitigated**: controlling the cpu usage percentage at 50%, it will trigger a memory alert only if the CPU remains at or above 50% consistently for 5 minutes. Virus/Malware
  - **Reliability**: Yes, this alert can generate a lot of false positives due to CPU spikes occuring when specfic integrations are initiated at the start of processing. HIGH
#### HTTP Request Size Monitor
Alert 3 is implemented as follows:
  - **Metric**: Packetbeat: http.request.bytes
  - **Threshold**: The sum of the requested bytes is over 3500 in 1 minute
  - **Vulnerability Mitigated**: By controlling the number of http request sizes thru filter, protection is enabled to detect/prevent DDOS attacks for IPS/IDS
  - **Reliability**: No, this alert doesnt generate an excessive amount of false positve because DDOS attacks submit requests within seconds, not within minutes. MEDIUM



### Suggestions for Going Further (Optional)
_TODO_: 
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
