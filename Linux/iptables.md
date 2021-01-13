## Настройка политики по умолчанию (таблица filter)

`sudo iptables -P INPUT DROP`

## Блокировка доступа к порту 22

`sudo iptables -i eth0 -A INPUT -p tcp --dport 22 -j DROP`

## Открыть доступа к порту 4444

`sudo iptables -i eth0 -I INPUT -p tcp --dport 4444 -j ACCEPT`

`-i eth0` - match packets on the eth0 interface
`-I INPUT` - insert the rule at the top of the INPUT chain
`-p tcp` - match TCP packets only
`--dport 4444` - match packets destined to port 4444
`-j ACCEPT` - accept the packet ("jump" to ACCEPT)

