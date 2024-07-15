---
title: "Overview of Information Security and Privacy"
author: Bryan Hoang
date: 12/11/2023
geometry: margin=2cm
output: pdf_document
---
<!-- pandoc example.md -o example.pdf -->

## 1.1 Key Security Concepts and Requirements

The NIST Computer Security Handbook defines *computer security* as follows: The protection afforded to an automated informmation system in order to attain the applicable objectives of preserving the **integrity, availability, and confidentiality** of information system resources; some examples include hardware, software, firmware, information/data, and telecommunications.

Integrity covers two related concepts: data integrity and system integrity. Data integrity assures that information and programs are changed only in a specified and authorized manner. System integrity assures that the system performs its intended function in an unimpaired manner, free from deliberate or inadvertent unauthorized manipulation of the system. A loss of integrity is the unauthorized modification or destruction of information.

Availability assures that the systems work promptly and service is not denied to authorized users. Loss of availability is the disruption of access to or use of information or an information system.

Confidentiality covers two related concepts: data confidentiality and privacy. Data confidentiality assures that private or confidential information isn't made available or disclosed to unauthorized individuals. Privacy assures that individuals control and influence what information related to them may be collected and stored by whom and to whom that information may be disclosed. Loss of confidentiality is the unauthorized disclosure of information.

These three concepts form what's known as the **CIA triad**.

Other concepts present in INFOSEC include authenticity and accountability. Authenticity refers to the property of being genuine and being able to be verified and trusted; confidence in the validity of a transmission, message, or message originator. Accountability refers to the security goal that generates the requirement for action of an entity to be trace uniquely to that entity.

There are several levels of impact from security breaches: low, moderate and high.  Low impact breaches have limited adverse effects on organizational operators, assets, or individuals. This means that depending on where the berach is, the loss of confidentiality, integrity, or availability might cause a degradation in mission capability but the organization is still able to perform its primary function. Moderate loss refers to a serious adverse effect on organization operations, assets, or individuals. It wil cause a significant degradation in mission capability. High losses are expected to have a severe or catastropic adverse effect on organizational operations, assets, or individuals. This means that the organization is not able to perform one or more of its primary functions.

Computer security is challenging for many different reasons:

- It's not simple because requirements seem to be straightforward but the mechanisms are complex.
- We must be able to predict potential attacks and vulnerabilities.
- Battle of wits between attackers and admins.
- It's not perceived to be beneficial to the organization until something breaks.
- Requires constant vigilance and monitoring.

## 1.2 Security Terminology and Architecture

In the context of security, our concern is with the vulnerabilities of system resources which may be corrupted (loss of integrity), become leaky (loss of confidentiality), or become unavailable (loss of availability). Corruption refers to the concept that system resources may do the wrong thing or give the wrong answers. Leaky refers to the concept that system resources may give out information that they shouldn't. Unavailable refers to the concept that system resources may not be available when they're needed.

Countermeasures deployed are never perfect and will always have residual vulnerability. In security, there are several ways countermeasures are used to protect against vulnerabilities:

- Prevent
- Detect
- Recover

The goal is to minimize risk given constraints.

### X.800 Security Architecture

X.800 defines a systematic way of defining requirements for security and characterizing the approaches to satisfying those requirements. It's useful to managers as a way of organizing the task of providing security. It focuses on security attacks, mechanisms, and services.

- Security Attack: any action that compromises the security of information owned by an organization.
- Security Mechanism: A mechanism that's designed to detect, prevent, or receover from a security attack.
- Security Service: A service that enhances the security of the data processing systems and the information transfers of an organization. These services are intended to counter security attacks.

The difference between security mechanism and security services is the security services use security mechanisms to provide the service. Security mechanisms are the tools used to provide security services.

### Security Attacks

They come in two flavors: passive attacks and active attacks. Passive attacks attempt to learn or make use of information from a system but don't affect system resources. Active attacks attempt to alter system resources or affect their operation.

Passive attaccks are in the nature of eavesdropping on, or monitoring of, transmissions. The goal of the opponent is to obtain information that's being transmitted. There are two types of passive attacks: release of message contents and traffic analysis. They're difficult to detect because they don't involve any alteration of the data. Therefore, our main goal is to prevent them.

Active attacks involve some modification of the data strem or creation of a false stream and can be subdivided into four major categories:

- Masqurade: one entity pretends to be a different entity.
- Replay: involves the passive capture of a data unit and its subsequent retransmission to produce an unauthorized effect.
- Modification of messages: some portion of a legitimate message is altered, or messages are delayed or reordered, to produce an unauthorized effect.
- Denial of service: prevents or inhibits the normal use or management of communications facilities.

Active attacks while preventable, are much more difficult due to the creativity of attackers. The goal is to detect and recover from any disruption caused by them.

### Security Services

According X.800, security services are a service provided by a protocol layer of communicating open systems, which ensures adequate security of the systems or data transfers.

SS use one or more security mechanisms. They often replicate functions normally associated with physical documents; for example, they have signatures, dates; need protection from disclosure, tampering, or destruction; be notarized or witnessed; be recorded or licensed.

There are five SS categories and 14 specific services given in X.800. The list includes various classic security services which are traditionally discussed.

- Authentication
  Authentication is concerned with assuring that the communication is authentic. There are two specific authentication services defined by X.800; peer entity authentication and data origin authentication. PE authentication provides corroboration or the identity of a peer entity in an association while DO authentication provides corroboration of the source of a data unit.
  I.e., assurance that communicating entity is the one claimed.

- Access Control
  AC is the ability to limit and control the access to host systems and applications via communication links.

- Confidentiality
  Confidentiality is the protection of transmitted data from passive attacks, and the protection of traffic flow from analysis.

- Integrity
  Integrity assures that the messages are received as sent, with no duplication, insertion, modification, replay, or loss.

- Availability
  Availability is the property that data is accessible and modifiable in a timely fashion by an authorized person.

### Security Mechanisms

These are features designed to detect, prevent, or receover from security attacks. No single mechanism supports all services required, however one particular element underlies many security mechanisms: cryptographic techniques.

There are two types of mechanisms: pervasive security mechanisms and specific security nechanisms.

Pervasive SMs are trusted functionality, seucrity labels, event detection, security audit trail, and security recovery. They're not specific to any particular OSI security service or protocol layer.

Specific SMs are cryptographic techniques, access control mechanisms, data integrity mechanisms, authentication exchange mechanisms, traffic padding, routing control, notarization, and physical security mechanisms. They're specific to a particular OSI security service or protocol layer.

### Computer Security Strategy

The first step in devising security services and mechanisms is to develop a security policy. Security policy is an informal description of desired system behavior. Such policies may reference requirements for security, integrity, and availability. They're also formal statements of rules and practices that specify or regulate how a system or organization provides security services to protect sensitive system resources.

To develop a security policy, managers need to consider the following factors:

- Value of assets being protected
- Vulnerabilities of the system
- Potential threats and likelihood of attacks

Security implementation involves four complementary courses of action:

- Prevention: An ideal security scheme is one in which no attack is successful. It's not practical in all cases, but there's a wide range of threats in which it's possible to prevent attacks.
- Detection: Absolute detection is not feasible in all cases, but it's practical to detect security attacks.
- Response: If a mechanism detects an ongoing attack, such as a DDOS attack, the system may be able to respond in a way to halt the attack and prevent further damage.
- Recovery: If an attack is successful, the system may be able to recover from the attack and restore the system to a secure state.

NIST defines assurance as the degree of confidence one has that the security measures, both technical and operational, work as intended to protect a system and its information.

Evlauation is the process of examining a product or system with respect to a certain criteria. It may involve testing or formal analytic or mathematical techniques.