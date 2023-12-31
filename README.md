# Building a Honeynet + SOC in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://imgur.com/TludXH6.jpg)

## Introduction

In this project,  I developed a compact honeynet within Azure and integrated log sources from a variety of resources into a Log Analytics workspace. This setup is utilized by Microsoft Sentinel to construct attack maps, initiate alerts, and generate incidents. Initially, I recorded security metrics in an unsecured environment for a 24-hour period. Following this, I implemented several security measures to fortify the environment and then monitored the same metrics for another 24 hours. The outcomes are presented below. The key metrics we'll be showcasing include:

- SecurityEvent: (Capturing Windows Event Logs)
- Syslog: (Documenting Linux Event Logs)
- SecurityAlert: (Alerts triggered in Log Analytics)
- SecurityIncident: (Incidents created by Microsoft Sentinel)
- AzureNetworkAnalytics_CL: (Tracking malicious flows permitted into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

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
![NSG Allowed Inbound Malicious Flows](https://imgur.com/z48qKB7.png)<br>
![Linux Syslog Auth Failures](https://imgur.com/36MoEzk.png)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/yqmYJXR.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics I measured in our insecure environment for 24 hours:
Start Time 2023-12-28 9:41:17
Stop Time 2023-12-28 9:41:17

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 23073
| Syslog                   | 2547
| SecurityAlert            | 6
| SecurityIncident         | 235
| AzureNetworkAnalytics_CL | 2389

## Attack Maps After Hardening / Security Controls

![NSG Allowed Inbound Malicious Flows](https://imgur.com/MKl9mcU.png)<br>
![Linux Syslog Auth Failures](https://imgur.com/c0VDd0J.png)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/nVQerDo.png)<br>

## Metrics After Hardening / Security Controls

The following table shows the metrics I measured in our environment for another 24 hours, but after I have applied security controls:
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

In this project initiative, I set up a small-scale honeynet within Microsoft Azure and linked various log sources to a Log Analytics workspace. Using Microsoft Sentinel, we generated alerts and incidents based on these logs. I also evaluated performance metrics in the network when it was not secure, and then again after implementing security measures. The results were significant.There was a substantial decrease in the number of security events and incidents post-implementation. This confirms the effectiveness of the security controls.

It's important to note that had there been extensive activity from regular users within the network. Then I was able to observed a higher number of security events and alerts in the 24-hour period after the security measures were put in place.
