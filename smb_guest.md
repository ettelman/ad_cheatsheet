enum4linux -a -u "" -p "" <dc-ip>  # enumerate shares, users,policys from smb with null
enum4linux -a -u "guest" -p "" <dc-ip> # same but with guest

smbmap -u "" -p "" -P 445 -H <dc-ip> # shows shares and permissions from null
smbmap -u "guest" -p "" -P 445 -H <dc-ip> # same but with guest

smbclient -U '%' -L //<dc-ip> # try to auth with null session
smbclient -U 'guest%' -L //<dc-ip> # same but with guest

netexec smb <ip> -u "" -p "" # enumerate null session
netexec smb <ip> -u 'a' -p "" # enumerate anonymous access

