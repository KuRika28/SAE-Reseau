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
interface e0/0 (connectée à DMZ)
ip address 54.98.153.194 255.255.255.192
no shutdown

interface e0/1 (connectée au switch)
ip address 54.98.152.129 255.255.255.128
no shutdown
end
```

### Sur Commercial :
```
conf term
interface e0/0 (connectée à DMZ)
ip address 54.98.153.195 255.255.255.192
no shutdown

interface e0/1 (connectée au switch)
ip address 54.98.152.1 255.255.255.128
no shutdown
end
```

### Sur Développement :
```
conf term
interface e0/0 (connectée à DMZ)
ip address 54.98.153.196 255.255.255.192
no shutdown

interface e0/1 (connectée au switch)
ip address 54.98.153.1 255.255.255.128
no shutdown
end
```

### Sur Recherche :
```
conf term
interface e0/0 (connectée à Développement)
ip address 54.98.153.2 255.255.255.128
no shutdown

interface e0/1 (connectée au switch)
ip address 54.98.153.129 255.255.255.192
no shutdown
end
```