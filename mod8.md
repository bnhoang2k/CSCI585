---
title: "Denial of Service Attacks"
author: Bryan Hoang
date: 12/12/2023
geometry: margin=2cm
output: pdf_document
---
<!-- pandoc example.md -o example.pdf -->

## DoS

Actions that prevent or impair the authorized use of networks, systems, or apps by exhausting resources such as CPUs, memory, etc.

## Classical ping flooding

Simplest classical DoS attack is a flooding attack on an org. The aim is to overwhelm the capacity of the network connection to the target org. If the attacker has access to a system with higher capacity network connection, then this system can likely generate a higher volume of traffic than the lower cpaacity target connection can handle.

### Source Address Spoofing

Packets used in many DoS attacks commonly use forged source addreses. This is known as source address spoofying.

Given suffciently privileged access to the network handling code on a computer system, i'ts easy to create packets with a forged source address. Given raw access to the network interface, the attacker now generates large volumes of packets. These would all have the target system as the destination adderss, but use randomly selected usually different source addresses for each packet.