## Why should you care about reverse shells?

* Reverse shells give attackers full control of the systems they are installed on
* Reverse shells allow attackers to collect and send your data out of your network
* Reverse shells allow attackers to capture usernames and passwords
* Reverse shells allow attackers to scan your network from the inside

## What is a shell?

* User inputs a command will be then executed by the system

## How do reverse shells work?

* Reverse shells force an internal system to actively connect out to an external system

## How do reverse shells get installed on your systems?

* Physical Access
  * Reverse shell installed using auto-play feature
  * Skilled intruder with private physical access can defeat all installed security mechanisms and install reverse shells
  * Insider installing reverse shells
* Social Engineering someone into installing the reverse shell program
* Users executing email attachments that install the reverse shell program
* Users downloading and executing reverse shell program
* Legitimate programs that can act like reverse shells

## What covert channels do reverse shells use?

* Reverse shells can operate using any protocol/port combination that is allowed out of your network

* Netcat – any TCP/UDP port

* Cryptcat - any TCP/UDP port with encryption

* Loki & Ping Tunnel - ICMP

* Reverse WWW Shell – HTTP

* DNS Tunnel – DNS

* Sneakin – Telnet

* Stunnel – SSL

* Secure Shell - SSH

* Custom Reverse Shell ???

## Reverse WWW Shell

* Attacker configures variables
  * External system IP address
  * Port
  * Time of day to execute
  * Proxy information needed
* Attacker must find a way to execute on the internal system

## What covert channels do reverse shells use?



