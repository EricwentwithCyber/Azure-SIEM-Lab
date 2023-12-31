# Azure-SIEM-Lab
Building a SIEM in Azure utilizing Microsoft Sentienl, Microsoft Defender, Log Anaytlics, NSGs, Kusto Query, Lanuage and more.

# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project,  I developed a compact honeynet within Azure and integrated log sources from a variety of resources into a Log Analytics workspace. This setup is utilized by Microsoft Sentinel to construct attack maps, initiate alerts, and generate incidents. Initially, I recorded security metrics in an unsecured environment for a 24-hour period. Following this, I implemented several security measures to fortify the environment and then monitored the same metrics for another 24 hours. The outcomes are presented below. The key metrics we'll be showcasing include:

- SecurityEvent: (Capturing Windows Event Logs)
- Syslog: (Documenting Linux Event Logs)
- SecurityAlert: (Alerts triggered in Log Analytics)
- SecurityIncident: (Incidents created by Microsoft Sentinel)
- AzureNetworkAnalytics_CL: (Tracking malicious flows permitted into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://tinypic.host/image/02LAz)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://tinypic.host/image/02bxU)

The architecture of the mini honeynet in Azure consists of the following components:

- Microsoft Sentinel
- Microsoft Entra
- Microsoft Defender
- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Network Diagram
- Compliance and Auditing
- Security Polices and Rules
- Monitoring and Alerting Strategies


For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://tinypic.host/image/02zr2)<br>
![Linux Syslog Auth Failures](https://tinypic.host/image/027n4)<br>
![Windows RDP/SMB Auth Failures](https://tinypic.host/image/02Qcf)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-12-28 9:41:17
Stop Time 2023-12-28 9:41:17

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 23073
| Syslog                   | 2547
| SecurityAlert            | 6
| SecurityIncident         | 235
| AzureNetworkAnalytics_CL | 2389

## Metrics After Hardening / Security Controls

![NSG Allowed Inbound Malicious Flows](https://tinypic.host/image/02wQk)<br>
![Linux Syslog Auth Failures](https://tinypic.host/image/02c5O)<br>
![Windows RDP/SMB Auth Failures](https://tinypic.host/image/02sSm)<br>

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-12-30 9:30:23
Stop Time	2023-12-30 9:30:23

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 22779
| Syslog                   | 43
| SecurityAlert            | 0
| SecurityIncident         | 10
| AzureNetworkAnalytics_CL | 152

## Conclusion

In this project initiative, we set up a small-scale honeynet within Microsoft Azure and linked various log sources to a Log Analytics workspace. Using Microsoft Sentinel, we generated alerts and incidents based on these logs. We also evaluated performance metrics in the network when it was not secure, and then again after implementing security measures. The results were significant: there was a substantial decrease in the number of security events and incidents post-implementation, confirming the effectiveness of the security controls.

It's important to note that had there been extensive activity from regular users within the network, we might have observed a higher number of security events and alerts in the 24-hour period after the security measures were put in place.
