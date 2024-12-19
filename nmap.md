# Nmap scripts

nmap -sP -p <ip> # ping scan
nmap -PN -sV --top-ports 50 --open <ip> # quick scan
nmap -PN --script smb-vuln* -p139,445 <ip> # search smb vuln
nmap -PN -sC -sV -oA <output> <ip> # classic scan
nmap -PN -sC -sV -p- -oA <output> <ip> # full scan
nmap -sU -sC -sV -oA <output> <ip> # udp scan

## Scan with no ping and output
nmap -sC -sV -Pn -p- -oA filename <ip> -vv
