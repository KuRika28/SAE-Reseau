## Configuration des interfaces des routeurs avec les adresses IP

### Sur Internet
```
conf term
interface e0/0 (connectée à Internet)
ip address 10.0.0.1 255.255.255.0
no shutdown
end
```

### Sur DHCP :
```
conf term
interface e0/0 (connectée à Internet)
ip address 10.0.0.6 255.255.255.0
no shutdown

service dhcp

ip dhcp pool land
network 54.98.153.0 255.255.255.128
lease 1
default-router 54.98.153.196
ip dhcp excluded-address 54.98.153.1 54.98.153.10

ip dhcp pool lanl
network 54.98.152.128 255.255.255.128
lease 1
default-router 54.98.153.194
ip dhcp excluded-address 54.98.152.129 54.98.152.138

ip dhcp pool lanc
network 54.98.152.0 255.255.255.128
lease 1
default-router 54.98.153.195
ip dhcp excluded-address 54.98.152.1 54.98.152.10

ip dhcp pool lanr
network 54.98.153.128 255.255.255.192
lease 1
default-router 54.98.153.196
ip dhcp excluded-address 54.98.153.129 54.98.153.138

ip dhcp pool landmz
network 54.98.153.192 255.255.255.192
lease 1
default-router 54.98.153.193
ip dhcp excluded-address 54.98.153.193 54.98.153.202
```

### Sur Commercial :
```
conf term
interface e0/0 (connectée à Internet)
ip address 10.0.0.4 255.255.255.0
no shutdown

interface e0/1 (connectée à LAN Commercial)
ip address 54.98.152.1 255.255.255.128
no shutdown
ip helper-address 10.0.0.6
end
```

### Sur DMZ
```
conf term
interface e0/0 (connectée à Internet)
ip address 10.0.0.2 255.255.255.0
no shutdown

interface e0/1 (connectée à DMZ)
ip address 54.98.153.193 255.255.255.192
no shutdown
ip helper-address 10.0.0.6
end
```

### Sur Libre-service :
```
conf term
interface e0/0 (connectée à Internet)
ip address 10.0.0.3 255.255.255.0
no shutdown

interface e0/1 (connectée à LAN Libre-service)
ip address 54.98.152.129 255.255.255.128
no shutdown
ip helper-address 10.0.0.6
end
```

### Sur Développement :
```
conf term
interface e0/0 (connectée à Internet)
ip address 10.0.0.5 255.255.255.0
no shutdown

interface e0/1 (connectée au LAN Développement)
ip address 54.98.153.1 255.255.255.128
no shutdown
ip helper-address 10.0.0.6
end
```

### Sur Recherche :
```
conf term
interface e0/0 (connectée à LAN Développement)
ip address 54.98.153.2 255.255.255.128
no shutdown

interface e0/1 (connectée à LAN Recherche)
ip address 54.98.153.129 255.255.255.192
no shutdown
ip helper-address 54.98.153.1
end
```

## Configuration des PC statiques
### Sur PCLS
```
ip 54.98.152.130/25
```

### Sur PCDS
```
ip 554.98.153.3/25
```

### Sur PCRS
```
ip 54.98.153.130
```

### Sur PCCS
```
ip 54.98.152.2/25
```

## Pare-feux
### Sur Libre-service
```
conf term
ip access-list standard ls
permit 10.0.0.1 0.0.0.255
deny any
end

conf term
interface e0/0
ip access-group ls in
end
```

### Sur Recherche
```
conf term
ip access-list standard r
permit 54.98.153.0 0.0.127
deny any
end

conf term
interface e0/0
ip access-group r in
end
```

## Relais DHCP