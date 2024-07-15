---
title: "User Authentication"
author: Bryan Hoang
date: 12/11/2023
geometry: margin=2cm
output: pdf_document
---
<!-- pandoc example.md -o example.pdf -->

## Slides

### Definition

User authentication is the process of verifying an identity claimed by or for a system entity.

### Authentication Process

The authentication process consists of two steps:

- Identification step: Presenting an identifier to the security system. Identifiers should be assigned carefully, since authenticated identities are the basis for other security services, such as access control services.
- Verification step: Presenting or generating authentication information that corroborates the binding between the entity and the identifier.

For example, user Alice Toklas could have the identifier ABTOKLAS. This information needs to be stored on any server or computer system that Alice wishes to use and could be known to system admins and other uses. A typical term of authentication information associated with this user ID is a password, which is kept secret (known only to Alice and the system). If no one is able to obtain or guess Alice's password, then the combination of Alice's user ID and password enables admins to set up Alice's access permissions and audit her acitivites.

In essence, identification is the means by which a user provides a claimed identity to the system; user authentication is the means of establishing the validity of the claim. User authentication is distinct from message authentication. As defined earlier, message authentication is a procedure that allows communicating parties to verify that the contents of the received message have not been altered and that the source is authentic.

### Means of User Authentication

There are four general means of authenticating a user's identity, which can be used alone or in combination:

- Something the individual knows (e.g., a password, a personal identification number (PIN), or answers to prearranged questions)
- Something the individual possesses (e.g., a physical key, a smart card, or a token device)
- Something the individual is (e.g., a biometric characteristic, such as a fingerprint, iris scan, or voice recognition)
- Something the individual does (dynamic biometrics): This includes recognition by voice pattern, handwriting characteristics, typing rhythm, and gait.

All have issues however. Attackers may be able to guess/steal passwords. They can also forge or steal tokens. Users may forget a password or lose tokens, etc.

### Password Security Problems

Text passwords prove to be the domination form of online user authentication. There are studies that're trying to find a way to replace text passwords due to the many problems that come with them.

One of the problems that arises comes from the "something you know" factor. For passwords to be secure, they must be very strong and complex. However, this makes it difficult for users to remember them. Users may write them down, which is a security risk. Users may also use the same password for multiple accounts, which is also a security risk.

There are several attack strategies that attackers can use, but we have (some) countermeasures:

- Offline dictionary attack: A determined hacker may bypass access controls and gain access to the system password file. The attacker then compares the password hashes against hashes of common passwords.
- Specific account attack: The attacker targets a specific account and submits password guesses until the correct password is found.
- Popular password attack: The attacker dchooses a popular password and tries it against a wide range of user IDs.
- Password guessing against single user: The attacker attempts to gain knowledge about the account holder and system password policies and uses that knowledge to guess the password.
- Workstation hijacking: The attacker waits until a logged-in workstation is unattended and then uses the workstation to access the system.

There are many others, but these are the most common. There are also countermeasures to these attacks:

- Stop unauthorized access to the password file.
- Intrusion detection systems can detect and respond to attacks.
- Account lockout mechanisms can prevent an attacker from making multiple guesses.
- Training users to choose strong passwords and to not write them down.
- Automatic workstation locking after a period of inactivity.
- etc.

### Use of Hashed Passwords at the Server-side

A widely used password seccurity technique is the use of hashed psswords and a salt value.  To load a new password into a system, the user selects or is assigned a password. This password is combined with a fixed-length salt value (so the same user password can create multiple hash values, depending on which salt is used). In older implementations, the salt is related to the time the password is assigned to the user. Newer implementations use a PRNG or random number.

The password and salt serve as inputs to a hashing algorithm to produce a fixed-length hash code. The hash algorithm is designed to be slow to execute to thwart attacks. The hashed password is then stored together with a plaintext copy of the salt in the password file for the corresponding user ID.

It's shown to be secure against cryptanalytic attacks. When users attempt to log onto a system, the user provides an ID and a password. The OS uses the ID to index into the password file and retrieve the plaintext salt and the encrypted password. The salt and user-supplied password are then used as an input to the hash algorithm. If the resulting hash code matches the stored hash code, the user is authenticated.

There are two problems associated with this scheme:

- First users can gain access tot a machine using a guest account (or by any other means) and then run a password guessing program to try and crack it.
- If the attacker is able to obtain a copy of the password, then a cracker program can be run on another machine at leisure. This'll allow the attacker to run through millions of possible passwords until the correct one is found.

### Password Cracking Approaches

- Dictionary Attacks: Try every possible password then obvious variants in a large dictionary against hash in password file.
- Rainbow table attacks: Precompute table of hash values of all possible passwords. These are HUGE; a 1.4 GB table cracks 99.9% of passwords of alphanumeric windows passowrds in 13.8 seconds.
  Luckily, these aren't feasible if larger salt values are used.

### Password File Access Control

Another way to stop password attacks is to deny attacker access to the password file.. If the hashed password portion of the file is accessible only by a privileged user, then the attacker cannot read it without already knowing the password of a privileged user.

Often, hashed passwords are kept in separate files from the user IDs referred to as a shadow password file. Special attention must be paid to keep this shadow file protected from unauthorized access.

There are still a number of vulnerabilities:

- OS bug exploits
- Error on permissions on password file making it world readable
- Users reuse same password on other systems which may be compromised and open up the password file to the attacker inadverently.
- Passwords may also be captured by sniffing network traffic.

### Password Countermeasures

The most common ways to deal with password vulnerabilities are:

- User education
  This is needed because studies have shown that many users choose passwords that are too short or easy to guess. Many users also write down their passwords, which is a security risk. Additionally, passwords that are complex are difficult to remember, so users may use the same password for multiple accounts.
- Reactive password checking
  When a system periodically run its own password cracker to guess guessable passwords, the system can cancel any passwords guessed and notify the user to choose a new password. This is a good way to prevent users from choosing weak passwords but it's costly to implement.
- Proactive password checking
  When users select a password, the system can check it it's allowable and reject it if it's not. The hardest part of this is that it must strike a balance between user acceptability and security. But it's the best way to prevent users from choosing weak passwords.

Some other popular solutions include graphical passowrds, password hashing systems, single sign-on systems, and browser-based password managers.

PwdHASH is a browser extension that is a pure browser-based solution. It uses the website domain name as a salt, and PwDHASH hashes a user's original PT password to generate a site password. The generate password will be used to log into a site. Even if users type in the same plain-text password on different websites, the generated password are all different. This prevents attackers from using a compromised password on other websites.

Biometric authentication can also be used, which is based on the user's physical characteristics. Compared to passwords and tokens, BA is both technically complex and expensive and have yet to mature as a standard tool for user authentication to computer systems.

In any biometric scheme, some physical characteristic of the individual is mapped into a digital representation. When users are authenticated, the system compares the stored template to the presented template. Given the complexities of physical characteristics, we cannot expect that there'll be an exact match between the stored and presented templates. Instead, the system must determine whether the presented template is sufficiently close to the stored template to be considered a match. Because of this, ther are problems for false matches and false nonmatches if two individuals have similar physical characteristics.

### Kerberos

Kerberos is an authentication service developed at MIT and is the most widely deployed trusted third party key distribution system. It provides centralized mutual authentication in a distributed network.

- It allows user access to distributed service in the network
- A workstation cannot be trusted to indetify its user
- Rather all trust a central authentication server
- Relies exclusively on symmetric encryption
- Requires a user to prove their identity for each service invoked, also requires ervers to prove their identity to the user

## The Quest to Replace Passwords: A Framework for Comparative Evaluation of Web Authentication Schemes

Main problem with passwords is that they must be usable but also secure. Many security experts are trying to find different ways of authentication that are more secure than passwords but also usable. The paper analyzes the usability and security of 12 different authentication schemes. Here's what they found:

- No scheme is perfect
- No scheme does better on one or more benefits than password
- Most schemes do better than passwords on security
- Some do better or worse on usability
- All do worse on deployability

It's hard to find a scheme that's better than passwords in all aspects: usability, security, and deployability.

