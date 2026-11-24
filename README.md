# 2c.SIMULATING ARP /RARP PROTOCOLS
## NAME: M AADHAVAN NAGARAJAN
## REGISTER NUMBER: 212225040001
## AIM:
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.

## PROGRAM - ARP
SERVER PROGRAM:
```

import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)

c, addr = s.accept()

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break

    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()
```
CLIENT PROGRAM:
```

import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    ip = input("Enter logical Address : ")

    if ip.lower() == "exit":
        break

    s.send(ip.encode())
    print("MAC Address", s.recv(1024).decode())

s.close()
```
## OUPUT - ARP
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0e72e67b-5e38-4907-8552-efddde674ed1" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/061ebabe-2b31-4ef3-b3b6-bbcdeddf7d47" />

## PROGRAM - RARP
SERVER PROGRAM:
```

import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)

c, addr = s.accept()

address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:
    mac = c.recv(1024).decode()

    if not mac:
        break

    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()
```
CLIENT PROGRAM:
```

import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    mac = input("Enter MAC Address : ")

    if mac.lower() == "exit":
        break

    s.send(mac.encode())
    print("Logical Address", s.recv(1024).decode())

s.close()
```
## OUPUT -RARP
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7bdc6120-c082-417a-bc76-1d66fa4386e1" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d07eb735-72c1-4243-a8ed-0c05832aec77" />

## RESULT
Thus the python program for simulating ARP protocols using TCP was successfully 
executed.
