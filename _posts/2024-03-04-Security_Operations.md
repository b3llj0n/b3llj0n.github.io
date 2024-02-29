---
layout: post
title: Introduction to Defensive Security part 2
date: 2024-03-04 10:00 +0700
categories: [TryHackMe, Introduction to Cyber Security]
tags: [Introduction to Cyber Security, Blue Team]     # TAG names should always be lowercase
img_path: '/assets/THM'
image: 
  path: logo.png
--- 

## Introduction to Security Operations

![image](https://github.com/zs0b/zs0b.github.io/assets/118095276/44e7e14b-f559-4297-9914-71b2a795b988)

A *Security Operations Center* (SOC) is a *team* of IT security professionals tasked with monitoring a company’s network and systems 24 hours a day, seven days a week. Their purpose of monitoring is to:

- **Find vulnerabilities on the network**: *A vulnerability is a weakness that an attacker can exploit to carry out things beyond their permission level. A vulnerability might be discovered in any device’s software (operating system and programs) on the network, such as a server or a computer. For instance, the SOC might discover a set of MS Windows computers that must be patched against a specific published vulnerability. Strictly speaking, vulnerabilities are not necessarily the SOC’s responsibility; however, unfixed vulnerabilities affect the security level of the entire company*.

- **Detect unauthorized activity**: *Consider the case where an attacker discovered the username and password of one of the employees and used it to log in to the company system. It is crucial to detect this kind of unauthorized activity quickly before it causes any damage. Many clues can help us detect this, such as geographic location*.

- **Discover policy violations**: *A security policy is a set of rules and procedures created to help protect a company against security threats and ensure compliance. What is considered a violation would vary from one company to another; examples include downloading pirated media files and sending confidential company files insecurely*.

- **Detect intrusions**: *Intrusions refer to system and network intrusions. One example scenario would be an attacker successfully exploiting our web application. Another example scenario would be a user visiting a malicious site and getting their computer infected*.

- **Support with the incident response**: *An incident can be an observation, a policy violation, an intrusion attempt, or something more damaging such as a major breach. Responding correctly to a severe incident is not an easy task. The SOC can support the incident response team handle the situation*.

This room focuses on the SOC services and everyday work. We recommend that you finish the Introduction to Defensive Security room before going through this one.

### What does SOC stand for?

`Security Operations Center`

### How many hours a day does the SOC monitor the network?

`24`

## Elements of Security Operations

In this task, we talk about:

- Example data sources that the SOC relies on

- The services that the SOC provides

- An example scenario.

### Data Sources
The SOC uses many data sources to monitor the network for signs of intrusions and to detect any malicious behaviour. Some of these sources are:

- **Server logs**: There are many types of servers on a network, such as a mail server, web server, and domain controller on MS Windows networks. Logs contain information about various activities, such as successful and failed login attempts, among many others. There is a trove of information that can be found in the server logs.

- **DNS activity**: DNS stands for Domain Name System, and it is the protocol responsible for converting a domain name, such as `tryhackme.com`, to an IP address, such as `10.3.13.37`, among other domain name related queries. One analogy of the DNS query is asking, “How can I reach TryHackMe?” and someone replying with the postal address. In practice, if someone tries to browse `tryhackme.com`, the DNS server has to resolve it and can log the DNS query to monitoring. The SOC can gather information about domain names that internal systems are trying to communicate with by merely inspecting DNS queries.

- `Firewall logs`: A firewall is a device that controls network packets entering and leaving the network mainly by letting them through or blocking them. Consequently, firewall logs can reveal much information about what packets passed or tried to pass through the firewall.

- `DHCP logs`: DHCP stands for Dynamic Host Configuration Protocol, and it is responsible for assigning an IP address to the systems that try to connect to a network. One analogy of the DHCP request would be when you enter a fancy restaurant, and the waiter welcomes you and guides you to an empty table. Know that DHCP has automatically provided your device with the network settings whenever you can join a network without manual configuration. By inspecting DHCP transactions, we can learn about the devices that joined the network.

These are some of the most common data sources; however, many other sources can be used to aid in the network security monitoring and the other tasks of the SOC. A SOC might use a Security Information and Event Management (SIEM) system. The SIEM aggregates the data from the different sources so that the SOC can efficiently correlate the data and respond to attacks.

![image](https://github.com/zs0b/zs0b.github.io/assets/118095276/967c45a5-f4e5-4972-ba21-04d8dd7fcb1a)

### SOC Services

SOC services include reactive and proactive services in addition to other services.

Reactive services refer to the tasks initiated after detecting an intrusion or a malicious event. Example reactive services include:

- **Monitor security posture**: This is the primary role of the SOC, and it includes monitoring the network and computers for security alerts and notifications and responding to them as the need dictates.

- **Vulnerability management**: This refers to finding vulnerabilities in the company systems and patching (fixing) them. The SOC can assist with this task but not necessarily execute it.

- **Malware analysis**: The SOC might recover malicious programs that reached the network. The SOC can do basic analysis by executing it in a controlled environment. However, more advanced analysis requires sending it to a dedicated team.

- **Intrusion detection**: An intrusion detection system (IDS) is used to detect and log intrusions and suspicious packets. The SOC’s job is to maintain such a system, monitor its alerts, and go through its logs as the need dictates.

- **Reporting**: It is essential to report incidents and alarms. Reporting is necessary to ensure a smooth workflow and to support compliance requirements.

Proactive services refer to the tasks handled by the SOC without any indicator of an intrusion. Example proactive services carried out by the SOC include:

- **Network security monitoring (NSM)**: This focuses on monitoring the network data and analyzing the traffic to detect signs of intrusions.

- **Threat hunting**: With threat hunting, the SOC assumes an intrusion has already taken place and begins its hunt to see if they can confirm this assumption.

- **Threat Intelligence**: Threat intelligence focuses on learning about potential adversaries and their tactics and techniques to improve the company’s defences. The purpose would be to establish a threat-informed defence.

Other services by the SOC include **cyber security training**. Many data breaches and intrusions can be avoided by raising users’ security awareness and arming them with solid security training.

### Example Scenario

One role in a SOC is the SOC analyst. A SOC analyst is responsible for network security monitoring and log management. Let’s consider the following scenario. While monitoring the network traffic, a SOC analyst notices a particular DNS query repeating every minute. This behaviour is not that of a user browsing the Internet, and every precisely one minute, they are making a new DNS query.

The SOC analyst checks the source of the DNS query and identifies the cause as one laptop on the network. They isolate it and inspect it for signs of infection; they discover a process (program) using DNS to communicate with a malicious server. Soon, they find out that the computer was infected after visiting a malicious website by reviewing the computer logs. As a result, the laptop began communicating with a malicious server by hiding the messages in DNS queries. The laptop is cleaned, and threat hunting starts to ensure that no other computers are infected.

### What does NSM stand for?

`Network security monitoring`

## Practical Example of SOC

![image](https://github.com/zs0b/zs0b.github.io/assets/118095276/889277b3-7d20-45ae-9d64-184cb9cf85c8)

We use a firewall to stop an ongoing attack in this task. A firewall is a device that inspects network packets entering and leaving a network or a system. The most basic types of firewalls inspect:

- **Source and destination IP addresses**: An IP address is a logical address that allows you to communicate over the Internet. One analogy is the postal address; for example, a company needs a valid postal address to send and receive parcels. Think of the IP packet as a mail parcel.

- **Source and destination port numbers** (where applicable): A computer has an IP address; furthermore, each program on the computer needs a port number to communicate over the network. Back to our analogy, a port number would be similar to a room number within a company.

A firewall rule might be similar to the following:

![image](https://github.com/zs0b/zs0b.github.io/assets/118095276/9ff643b2-7a11-488a-b49b-1dc79fb75474)

The above two rules dictate the following:

- All IP packets from the source IP address `172.16.4.1` to the destination IP address `10.10.10.41` to the destination port number `80` will be allowed; hence PASS.

- All IP packets from the source IP address `172.16.8.1` to the destination IP address `10.10.10.81` to the destination port number `23` will be blocked; hence DROP.

Click on “View Site” to begin the simulation. As a member of the SOC team, while monitoring the network and systems, you notice one malicious IP address attacking one of the company’s computers. It seems that they are targeting many destination ports with malicious packets. It seems best if we block them at the firewall level.

### Add the necessary firewall rules to block the ongoing attack. What is the flag that you have received after successfully stopping the attack?

Add Firewall Rule

![image](https://github.com/zs0b/zs0b.github.io/assets/118095276/adcd1051-9652-45e6-9843-51e7edf6ab4c)

![image](https://github.com/zs0b/zs0b.github.io/assets/118095276/7ec8b646-85e9-4b89-a65b-d14842ca4176)

`THM{ATTACK_BLOCKED}`

goodbye, thank you for reading until now //~//










































