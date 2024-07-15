---
title: "Intrusion Detection"
author: Bryan Hoang
date: 12/12/2023
geometry: margin=2cm
output: pdf_document
---
<!-- pandoc example.md -o example.pdf -->

## Slides

### Intruders

A significant security problem for networked systems is hostile/unwatned, tresspass by users or software. User tresspass can take the form of unauthorized logon to a machine, or in the case of an authorized user, acquisition of privileges or performance of actions beyond those have been authorized.

Software tresspass can take the form of a virus, worm, or trojan horse. There are many types of intruders and they can be benign to serious.

There are three types of intruders:

- Masquerader: Individuals, likely an outsider, not authorized to use the computer and who penetrates a system's access controls to exploit a legitimate user's account.
- Misfeasor: A legitimate user, generally an insider, who accesses data, programs, or resources for which such access is not authorized, or who is authorized for such access but misuses his or her privileges.
- Clandestine user: An individual who seizes supervisory control of the system and uses this control to evade auditing and access controls or to suppress audit collection.

There are several types of intrusion:

- Remote root compromise
- Web server defacement
- Guessing/cracking passwords
- Copying/viewing sensitive data and DBs
- Viewing sensitive data without authorization

We define *security intrusion* and *intrusion detection* as follows:

- Security intrusion: A security event or combination of multiple security events, that constitute a security incident in which an intruder gains, or attempts to gain, access to a system without having authorization to do so.
- Intrusion detection: A security service that monitors and analyzes system events in real time for the purpose of finding, and providing real-time or near real-time warning of, attempts to access system resources in an unauthorized manner.

### Intruder Behavior Patterns

Techniques and behavior patterns of intruders are constantly shifting, to exploit newly discovered weaknesses and to evade detection and countermeasures. However, intruders typically use ssteps from a common attack methodology.

In essence, they exploit vulnerabilities, gain or increase privileges, evade detection, and cover their tracks. The following are the steps of an attack:

- Target acquisition and information gathering: Where the attackers identify and characterize the target systems using publicly available information, both technical and non-technical, and the user of network exploration tools to map target resources.
- Initial access: Where the attackers gain access to the target system, typically by exploiting a vulnerability in the target system or in a system accessible from the target system. They typically exploit remote network vulnerabilities by guessing weak authentication credentials or via the installation of malware on the system using some form social engineering.
- Privilege escalation: Where the attackers attempt to increase their privileges on the target system once initial access has been achieved. They typically exploit local vulnerabilities to gain root or administrator privileges.
- Information Gathering or System Exploit: Actions by the attacker to access or modify information on resources on the system, or to navigate to another system.
- Maintaining Access: Actions by the attacker to maintain access to the system, such as installing a backdoor or rootkit.
- Covering Tracks: Actions by the attacker to cover their tracks, such as deleting log files or modifying audit trails.

### Types of Intruders

- Hackers
  Motivated by thrill of access and status; targets "intereresting" or hard to hack places for fun. Don't "usually do it for malicious reasons."
  IDS/IPS useful to detect and prevent attacks.

- Cyber Criminals
  Motivated by financial gain, identity theft, corporate espionage, data theft, etc. Use malware to steal credit card numbers, bank account info, etc.
  IDS/IPS useful to detect and prevent attacks.

- Insiders
  Motivated by revenge, greed, or ideology. Have legitimate access to the system, but abuse it. Can be difficult to detect.
  IDS/IPS useful to detect and prevent attacks, but need more protection. Use access controls and principle of least privilege to prevent employees from accessing sensitive data. Use monitor logs and strong authentication to detect unauthorized access.

### Intrusion Detection Systems (IDS)

There are several IDS types:

- Host-based IDS: Monitors the characteristics of a single host adn the events occurring within that host for suspicious activity.
  It has good visibility, but it's highly suspectible to compromise.
- Network based IDS: Monitors network traffic for particular network segments or devices and analyzes network, transport, and application protocols to identify suspicious activity.
  It has limited visibility and its suspectible to evasion, but it's not easily compromised.
- Sensors: Devices responsible for colecting data. Inputs for sensors may be any part of a system that could contain evidence of intrusion. Example types of inputt to a sensor are network packets, log files, and system call traces. Sensors collect and forward this information to analyzers.
- Analyzers: Devices responsible for analyzing data collected by sensors to determine whether an intrusion has occurred. The output includes evidence supporting the conclusion that intrusion occurred and may provide guidance on what actions to take in response to the intrusion.
- User Interface: The user interface to an IDS enables users to view outputs from a system or control the behavior of a system.

The key motivation for IDS is to reduce damages, deter intruders, and support intrustion prevention systems (IPS).

### IDS Principles

For IDS to work, it's based on the assumption that the behavior of intruders differ from that of legitimate users in ways that're quantifiable. Due to the complexities and intricacies of human behavior, we can't expect that there'll be a crisp and exact distinction between an attack by an intruder and normal use of resources by an authorizer user.

Rather, we can expect some overlap. Patterns of legitimate user behavior can be established by observing past history, and significant deviation from such patterns can possibly be detected.

Using this method of testing for "differences" in normal behavior, it'll lead to a number of false positives or authorized users identified as intruders. On the other hand, an attempt to limit false positives by a tight interpretation of intruder behavior will lead to an increase in false negatives, or intruders not identified as intruders.

I.e., loose interpretations of intruder behavior will lead to more false positives, while tight interpretations of intruder behavior will lead to more false negatives. This is because if we interpret the overlap in loose behavior too loosely, we'll identify more authorized users as intruders, and if we're too tight, we'll identify less intruders as intruders.

IDS must:

- Run constantly with minimal human supervision
- Be fault tolearant such that it's able to recover from system crashes and reinitialization
- Resist subversion by intruders meaning it must monitor itself for signs of compromise
- Impose minimal overhead on system resources
- Configure according to system security policies
- Adapt to change in system and users
- Scale to monitor large number of systems
- Provide graceful degradation of service in the senes that if some component of it stops working for any erason, the rest of them must continue to function
- Allow dynamic reconfiguration is that ability to reconfigure without stopping the system

### Host-Based IDS

Host-Based IDs are specialized software used to monitor system activties to detect suspicious behavior. It's primary purpose is to detect intrusions, log suspicious events, and send alerts.

The primary benefit of a host-based IDS is that it can detect both external and internal intrusions, which is soemthing not possible either with network-based IDSs or firewalls.

They have two main techniques when it comes to detecting intrusions:

- Signatured-Based Detection: Defines a set of rules or attack patterns used to decide that a given behavior is that of an intruder or not. It attempts to define improper behavior and might be able to recognize events and sequences that, in context, reveal penetration.
- Anomaly Detection: Involves the collection of data relating to the behavior of legitimate users over a period of time. Then statistical tests are applied to observed behavior to determine witha high level of confidence whether that behavior is not legitimate user behavior.

I.e., anomaly approaches attempt to define normal or expect behavior. It's effective against masqueraders who're unlikely able to perfectly mimic behavior patterns of legitimate users. Such techniques however are unable to deal with misfeasors (insiders).

I.e., signature based detection matches input events against predefined signatures of malicious users; similar to virus scanning. It can identify attacks with acceptable accuracy and fewer false alarms than anomaly based systems, but cannot detect new intrusions unless given the information - false negatives are common.

Anomaly detection on the other hand watches for deviation of actual behavior from established profiles and classifies all abnormal activities as malicious. It can detect new unknown intrusions, but there the false positives are big issues. It can't tell when "new users" are added to systems.

### Audit Records

Audit records are a fundamental tool for intrusion detection; they're records of ongoing activity by users and must be maintained as input to an IDS. Basically there are two variants of them:

- Native audit records: Virtually all multi-user OS include accounting software that collects information on user activity. The advantage of using this information is that no additional collection software is needed. The disadvantage is that native audit records may not contain the needed information, or may not contain it in a convenient form.
- Detection-specific AR: A collection facility can be implemented that generates AR containing only that information required by the IDS. One advantage is that it could be made vendor independent and ported to a variety of systems. However, there is extra overhead having it.

### Distributed Host-Based IDS

Work on host-based IDSs focus on single-system stand-alone facilities. More effective defense on a distributed collection of hosts support by a LAN or internetwork can be achieved by coording and cooperation among IDSs across the network.

![distributed](image.png)

- Host agaent module: An audit collection module operating as a background process on a monitored system. Its purpose is to collect data on security-related events and transmit it to the central manager.
- LAN Monitor Agent Module: Operates in the same fashion as ahost agent module except it analyzes LAN traffic and reports the results to the central manager.
- Central Manager: Receives reports from lan monitor and host agents and processes and tries to correlate them to detect intrusions. It also provides a user interface to the IDS.

### Network-Based IDS

Network-based IDS monitor traffic at selected points on a network. They can examine traffic packet by packet in real time to detect intrusion patterns. NIDS may examin network, transport, and/or app level protocol activity directed toward systems.

The main difference is that NIDS examines packet traffic directed towards potentially vulnerable computer systems on a network. Host-based systems examine user and software activity within a host.

They're comprised by a number of sensors:

- Inline mode: Sensors are placed possible as part of other net devices, or atand alone where normal traffic must past through.
- Passive mode: Sensors are placed in a promiscuous mode on a network segment and monitor traffic without interfering with it. Passive sensors monitor copies of traffic, not the actual traffic.

They can be placed in many spots on a network. The "closer" they are to the internet (meaning that traffic isn't being filtered through external firewalls or internet firewalls), the more overhead they'll have to deal with. However, more external IDS can't detect internal attacks. The closer they are to the internal network, the more they can detect internal attacks.

### Honeypots

Honeypots are decoy systems designed to lure potential attackers away from critical systems. They're filled with fabricated info, instrumented with monitors /event loggers, and lure/hold attackers to collect activity info without exposing production systems.

Where they're deployed on networks matter:

![honeypots](image-1.png)

- Outside of external firewall: Useful for tracking attempts to connect to unused IP addresses within the scope of a network. It has little or no ability to trap internal attackers however.
- DMZ: The security admin must assure that other systems in the DMZ are secure against activity generated by the honeypot. It can be used to detect attacks against the DMZ, but it has little or no ability to trap internal attackers.
- Inside the internal firewall: It can be used to detect attacks against the internal network, but it has little or no ability to trap external attackers. There's a risk that an attacker could use the honeypot to attack other systems on the internal network.

### SNORT

Open source, highly configurable, and portable host-based or network-based IDS. It can pe rform real-time packet capture, protocol analysis, and content searching and matching.

SNORT can serve as a IPS or IDS. SNORT installations consist of a number of components:

- Decoder: Efficiently processes each captured packet to identify and isolate protocol headers at the data link, network, transports, and application layers.
- Detection Engine: Does actual work of inspecting packets for signs of intrusion. It's comprised of a number of preprocessors and detection plugins.
- Logger: Logs each packet that matches a rule if specified.
- Alert System: Generates alerts based on rules that match packets.

Rules in snort use a simple, flexible rule definition language with fixed head and zero or more options. The head includes: action, protocol, source IP, source PORT, direction, dest IP, dest PORT

An example rule is:

```snort

Alert tcp $EXTERNAL_NET any -> $HOME_NET any \
(msg: "SCAN SYN FIN"; flags: SF,12; \
reference: arachnids, 198: classtype: attempted-recon;)

```

## Paper

SNORT is lightweight, open-sourced, low-maintenance, and easy to understand. Most IDS/IPS are expensive, proprietary, and difficult to understand. SNORT is good for simple, lightly utilized networks where it doesn't make financial sense to spend so much on security. It can also be used as a supporting element to more complex IDS/IPS.

However, SNORT is reliant on signature-based detection, meaning it can't detect new attacks. It's also not very scalable, meaning it can't be used for large networks. It's also not very good at detecting insider attacks. It also needs to be ran behind a firewall. It's also ineffective if the payload is encrypted.

