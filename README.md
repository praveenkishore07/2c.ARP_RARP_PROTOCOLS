# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
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
**SERVER**
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Server is listening...")
c, addr = s.accept()

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    print(f"Received IP: {ip}")
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())

```
**CLIENT**
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter IP Address: ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())
```

## OUPUT - ARP
**server**
<img width="636" height="183" alt="arpserver" src="https://github.com/user-attachments/assets/21bb5258-745d-41b7-a5f6-3149fe674907" />
**client**
<img width="640" height="207" alt="arpclient" src="https://github.com/user-attachments/assets/96341e29-0817-4f15-9137-f3ac1227f3e0" />

## PROGRAM - RARP
**SERVER**
```
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is listening...")
c, addr = s.accept()

address = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    print(f"Received MAC: {mac}")
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())
```
**CLIENT**
```
import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter MAC Address: ")
    s.send(mac.encode())
    print("IP Address:", s.recv(1024).decode())
```

## OUPUT -RARP
**server**
<img width="633" height="200" alt="rarpserver" src="https://github.com/user-attachments/assets/bf86309d-ad47-49df-8685-18554a167cef" />
**client**
<img width="638" height="232" alt="rarpclient" src="https://github.com/user-attachments/assets/8e210f9f-3fd8-4238-8f48-97fb912e4f22" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
