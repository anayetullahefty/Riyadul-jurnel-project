## Task 2
I teamed up with Mamonur Rashid for this task, focusing on our network project that includes PCs, routers, and LANs. We selected four security objectives from the NIST Cyber Security Framework to help safeguard our system and spot potential problems, and here’s what we decided on and why they’re important for our setup:

- **Function: Protect; Category: Identity Management, Authentication, and Access Control (PR.AC); Sub-category: PR.AC-1 (Access permissions are managed, incorporating the principles of least privilege and separation of duties)**  
  We need this because it helps us manage who can get into our network devices, like the PCs and routers. If someone who shouldn’t be there gets access, they might change settings or take data, so this stops attacks like unauthorized access by only letting users do what they need, like keeping PC users on their own LAN.

- **Function: Protect; Category: Data Security (PR.DS); Sub-category: PR.DS-5 (Protections against data leaks are implemented)**  
  Protecting the info on our PCs, such as configuration files and user data, is a big deal for our project because it’s stored everywhere across the network. This objective helps stop data leaks, which could happen if someone hacks into a router or PC. It mitigates vulnerabilities like eavesdropping on the WAN link between Router 1 and Router 2.

- **Function: Detect; Category: Security Continuous Monitoring (DE.CM); Sub-category: DE.CM-1 (The network is monitored to detect potential cybersecurity events)**  
  Monitoring our network is crucial to spot problems early, especially with traffic moving between `14.59.1.0/24` and `14.22.1.0/24`. This helps us catch attacks like a denial-of-service (DoS) attempt that could slow down our routers, keeping the system safe by alerting us to weird activity.

- **Function: Detect; Category: Detection Processes (DE.DP); Sub-category: DE.DP-4 (Event detection information is communicated to appropriate personnel)**  
  This is useful because if something goes wrong—like a breach on PC1—we need to let the right people (like me or Mamonur) know fast. It mitigates risks from delayed responses to attacks, such as malware spreading across the network, by ensuring we get the info to act quickly.

## Task 3

I revisited the assets for our network project with Mamonur Rashid. We expanded it to cover all six asset types, adding details like fake MACs and serials since we don’t have real ones. For Data assets, I included classifications based on value and access, plus protections like CIA (Confidentiality, Integrity, Availability). Below are the updated tables:


### Data Assets
| Asset Name         | Identifying Info       | Classification (Value/Access) | Important Protections         |
|--------------------|-----------------------|-------------------------------|--------------------------------|
| Network Config Files | File ID: CFG-101      | High Value / Restricted       | Confidentiality, Integrity    |
| User Credentials   | File ID: CRED-102     | High Value / Confidential     | Confidentiality, Availability |
| Packet Logs        | File ID: PKT-103      | Medium Value / Internal       | Integrity, Availability       |
| System Backups     | File ID: BKP-104      | High Value / Restricted       | Confidentiality, Availability |

### Hardware Assets
| Asset Name         | Identifying Info       | Location                  |
|--------------------|-----------------------|---------------------------|
| Router 1           | Serial: R1-9876, MAC: 00:11:3C:22:5E:22 | LAN 1 (14.59.1.254)       |
| Router 2           | Serial: R2-5432, MAC: 11:e4:44:4D:22:7G | LAN 2 (14.22.1.254)       |
| Switch 1           | Serial: S1-1122, MAC: 45:2B:3C:4D:5E:4g | LAN 1                     |
| Switch 2           | Serial: S2-3344, MAC: 87:2B:5k:4D:6g:95 | LAN 2                     |
| PC1                | Serial: PC1-5566, MAC: 65:2B:3C:5s:5E:5h | LAN 1 (14.59.1.1)         |
| PC4                | Serial: PC4-7788, MAC: 4f:2B:4h:6d:5E:2K | LAN 2 (14.22.1.1)         |

### Software Assets
| Asset Name         | Identifying Info       | Version         |
|--------------------|-----------------------|-----------------|
| Router OS          | ID: OS-R1, License: LIC-901 | v3.2.1          |
| Firewall Software  | ID: FW-001, License: LIC-902 | v5.0.4          |
| Monitoring Tool    | ID: MON-002, License: LIC-903 | v2.3.7          |
| PC Operating System | ID: OS-PC1, License: LIC-904 | Ubuntu 24.04    |

### Network Assets
| Asset Name         | Identifying Info       | Bandwidth       |
|--------------------|-----------------------|-----------------|
| LAN 1 Network      | IP Range: 14.59.1.0/24 | 1 Gbps          |
| WAN Connection     | IP Range: 10.0.0.0/24  | 1 Gbps          |
| LAN 2 Network      | IP Range: 14.22.1.0/24 | 1 Gbps          |
| VLAN Segment       | VLAN ID: VLAN-10       | 100 Mbps        |

### Personnel Assets
| Asset Name         | Identifying Info       | Role            |
|--------------------|-----------------------|-----------------|
| Customer 1    | Customer ID: 202501   | Network Admin   |
| Customer 2     | Customer ID: 202502   | Security Analyst|
| IT Support Staff   | Employee ID: IT-001    | Support Tech    |

### Facility Assets
| Asset Name         | Identifying Info       | Location        |
|--------------------|-----------------------|-----------------|
| Data Center        | Room ID: DC-101        | Building K, Floor 5 |
| Network Hub Room   | Room ID: NH-102        | Building L, Floor 7 |
| Backup Storage     | Room ID: BS-103        | Building M, Floor 6 |
