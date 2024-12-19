## Get users on domain 

enum4linux -U <dc-ip> | grep 'user:'

netexec smb <ip> --users

net rpc group members 'Domain Users' -W '<domain>' -I '<ip>' -U '%'

nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='<domain>',userdb=<users_list_file>" <ip>

OSINT – enumerate username on internet

