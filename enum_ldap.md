ldapsearch -x -h ip -s base
nmap -n -sV --script "ldap* and not brute" -p 389 dcip
