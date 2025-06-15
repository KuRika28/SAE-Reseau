## Configuration des interfaces des routeurs avec les adresses IP

### Sur Internet
```
conf term
interface e0/0
ip address 54.98.153.194 255.255.255.224
no shutdown

interface e0/1
ip address 10.0.0.1 255.255.255.0
no shutdown
end

conf term
router rip
version 2
no auto-summary
network 54.98.153.192
network 10.0.0.0
end
```

### Sur DHCP :
```
conf term
interface e0/0
ip address 54.98.153.227 255.255.255.224
no shutdown
end

conf term
router rip
version 2
no auto-summary
network 54.98.153.224
end

conf term
service dhcp

ip dhcp pool land
network 54.98.153.0 255.255.255.128
lease 1
default-router 54.98.153.1
ip dhcp excluded-address 54.98.153.1 54.98.153.10

ip dhcp pool lanl
network 54.98.152.128 255.255.255.128
lease 1
default-router 54.98.152.129
ip dhcp excluded-address 54.98.152.129 54.98.152.138

ip dhcp pool lanc
network 54.98.152.0 255.255.255.128
lease 1
default-router 54.98.152.1
ip dhcp excluded-address 54.98.152.1 54.98.152.10

ip dhcp pool lanr
network 54.98.153.128 255.255.255.192
lease 1
default-router 54.98.153.129
ip dhcp excluded-address 54.98.153.129 54.98.153.138

ip dhcp pool landmz
network 54.98.153.192 255.255.255.224
lease 1
default-router 54.98.153.193
ip dhcp excluded-address 54.98.153.193 54.98.153.202
end
```

### Sur Commercial :
```
conf term
interface e0/0 
ip address 54.98.153.226 255.255.255.224
no shutdown

interface e0/1 
ip address 54.98.152.1 255.255.255.128
no shutdown
ip helper-address 54.98.153.227
end

conf term
router rip
version 2
no auto-summary
network 54.98.152.0
network 54.98.153.224
end
```

### Sur DMZ
```
conf term
interface e0/0
ip address 54.98.153.225 255.255.255.224
no shutdown

interface e0/1
ip address 54.98.153.193 255.255.255.224
no shutdown
ip helper-address 54.98.153.227
end

conf term
router rip
version 2
no auto-summary
network 54.98.153.192
network 54.98.153.224
network 10.0.0.0
end
```

### Sur Libre-service :
```
conf term
interface e0/0
ip address 54.98.153.228 255.255.255.224
no shutdown
ip helper-address 54.98.153.227

interface e0/1
ip address 54.98.152.129 255.255.255.128
no shutdown
ip helper-address 54.98.153.227
end

conf term
router rip
version 2
no auto-summary
network 54.98.152.128
network 54.98.153.224
end
```

### Sur Développement :
```
conf term
interface e0/0
ip address 54.98.153.229 255.255.255.224
no shutdown

interface e0/1
ip address 54.98.153.1 255.255.255.128
no shutdown
ip helper-address 54.98.153.227
end

conf term
router rip
version 2
no auto-summary
network 54.98.153.0
network 54.98.153.224
network 54.98.153.128
end
```

### Sur Recherche :
```
conf term
interface e0/0
ip address 54.98.153.2 255.255.255.128
no shutdown

interface e0/1 
ip address 54.98.153.129 255.255.255.192
no shutdown
ip helper-address 54.98.153.227
end

conf term
router rip
version 2
no auto-summary
network 54.98.153.128
network 54.98.153.0
end

```

## Configuration des PC
### Sur PCLS
```
ip 54.98.152.130/25 54.98.152.129
```

### Sur PCDS
```
ip 54.98.153.3/25 54.98.153.1
```

### Sur PCRS
```
ip 54.98.153.130/26 54.98.153.129
```

### Sur PCCS
```
ip 54.98.152.2/25 54.98.152.1
```

### Sur SERVEUR1
```
ip 54.98.153.195/27 54.98.153.193
```

### Sur PCInternet
```
ip 10.0.0.2/24 10.0.0.1
```

## Pare-feux
### Sur Libre-service
```
conf term
ip access-list standard ls
permit 10.0.0.0 0.0.0.255
permit 54.98.153.192 0.0.0.63
permit 54.98.153.224 0.0.0.0
permit 54.98.152.128 0.0.0.127
deny any
end

conf term
interface e0/1
ip access-group ls in
end
```

### Sur Recherche
```
conf term
ip access-list extended rEtendue
permit ip 54.98.153.0 0.0.0.127 54.98.153.128 0.0.0.63
deny ip 54.98.153.128 0.0.0.63 any
permit ip any any
end

conf term
interface e0/0
ip access-group rEtendue in
interface e0/1
ip access-group rEtendue in
end
```

### Sur DMZ
```
conf term
ip access-list extended dmzEtendue
deny ip 54.98.153.192 0.0.0.31 any
permit ip any 54.98.153.192 0.0.0.31
permit ip 54.98.152.128 0.0.0.127 10.0.0.0 0.0.0.255
permit ip 10.0.0.0 0.0.0.255 any
end

conf term
interface e0/0
ip access-group dmzEtendue in
end
```
