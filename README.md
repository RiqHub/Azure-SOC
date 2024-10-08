

# Building a SOC + Honeynet in Azure (Live Traffic)
![Design](https://github.com/user-attachments/assets/93cb9a71-b8fc-4587-9fe4-f26465280b9e)


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 48 hours, apply some security controls to harden the environment, measure metrics for another 48 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

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
<b>NSG Allowed Inbound Malicious Flows</b>![nsg](https://github.com/user-attachments/assets/baad78df-0470-4c64-8ab3-cda99bcf75bd)

<b>Linux Syslog Auth Failures</b>![linux](https://github.com/user-attachments/assets/fa317461-ca9f-467f-b288-6287f8c1e69b)

<b>Windows RDP/SMB Auth Failures</b>![Windows rdp](https://github.com/user-attachments/assets/4ba159ed-7cee-4bcb-8b06-b581c983c230)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 48 hours:

![Screenshot 2024-09-21 185743](https://github.com/user-attachments/assets/1b8d0be5-3d7a-4ea5-8705-3455a0c9ebbc)


## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 48 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 48 hours, but after we have applied security controls:

![Screenshot 2024-09-21 185759](https://github.com/user-attachments/assets/2f76181d-6d4b-4f65-b99a-7ff22e4f88d3)


## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 48-hour period following the implementation of the security controls.
