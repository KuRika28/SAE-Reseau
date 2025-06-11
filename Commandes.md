## Configuration des interfaces des routeurs avec les adresses IP

### Sur DMZ
```
conf term
interface e0/0 (connectée au switch)
ip address 54.98.153.193 255.255.255.192
no shutdown

.
.
.
end
```

### Sur Libre-service :
```
conf term
interface e0/0 (connectée au switch)
ip address 54.98.153.194 255.255.255.192
no shutdown

interface e0/1 (connectée à LAN Libre-service)
ip address 54.98.152.129 255.255.255.128
no shutdown
end
```

### Sur Commercial :
```
conf term
interface e0/0 (connectée au switch)
ip address 54.98.153.195 255.255.255.192
no shutdown

interface e0/1 (connectée à LAN Commercial)
ip address 54.98.152.1 255.255.255.128
no shutdown
end
```

### Sur Développement :
```
conf term
interface e0/0 (connectée au switch)
ip address 54.98.153.196 255.255.255.192
no shutdown

interface e0/1 (connectée au LAN Développement)
ip address 54.98.153.1 255.255.255.128
no shutdown
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
end
```

### Sur DHCP :
```
conf term
service dhcp

ip dhcp pool land
network 54.98.153.0 255.255.255.128
lease 1
default-router 54.98.153.196

ip dhcp pool lanl
network 54.98.152.128 255.255.255.128
lease 1
default-router 54.98.153.194

ip dhcp pool lanc
network 54.98.152.0 255.255.255.128
lease 1
default-router 54.98.153.195

ip dhcp pool lanr
network 54.98.153.128 255.255.255.128
lease 1
default-router 54.98.153.196
```