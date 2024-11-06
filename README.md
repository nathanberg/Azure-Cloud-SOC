# Building a SOC + Honeynet in Azure (Live Traffic)
PlaceHolder


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
PlaceHolder


## Architecture After Hardening / Security Controls
PlaceHolder


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
### NSG Allowed Inbound Malicious Flows
<img width="1282" alt="before_nsg-malicious-allowed-in" src="https://github.com/user-attachments/assets/a4a7b976-5ee2-45a6-ac08-77e34455ce45">

### Linux Syslog Auth Failures
<img width="1203" alt="before_linux-ssh-auth-fail" src="https://github.com/user-attachments/assets/091b6b8b-eed4-49f5-b213-ad31c5df2c6d">

### Windows RDP/SMB Auth Failures
<img width="1207" alt="before_windows-rdp-auth-fail" src="https://github.com/user-attachments/assets/db9512cc-9be5-44ec-be41-c7e459296f15">

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:



Start Time Saturday, November 2, 2024 at 11:30:29 PM UTC
Stop Time Sunday, November 3, 2024 at 11:30:29 PM UTC

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 33882
| Syslog                   | 46175
| SecurityAlert            | 0
| SecurityIncident         | 237
| AzureNetworkAnalytics_CL | 4240

### 
## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time Monday, November 4, 2024 at 11:33:50 PM UTC
Stop Time Tuesday, November 5, 2024 at 11:33:50 PM UTC


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8
| Syslog                   | 10
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
