# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### Server:
```
import socket

s = socket.socket()

s.connect(('localhost', 8000))

while True:

    data = s.recv(1024).decode()

    if not data:
        break

    print("Received Frames:", data)

    s.send("Acknowledgement received".encode())

s.close()
```
### Client:
```
import socket

s = socket.socket()

s.bind(('localhost', 8000))
s.listen(5)

c, addr = s.accept()

size = int(input("Enter number of frames to send: "))
frames = list(range(size))

window_size = int(input("Enter Window Size: "))

start = 0

while start < len(frames):

    end = start + window_size

    c.send(str(frames[start:end]).encode())

    ack = c.recv(1024).decode()

    if ack:
        print(ack)

    start += window_size

c.close()
s.close()
```
## OUPUT

<img width="1487" height="948" alt="Screenshot 2026-05-19 183614" src="https://github.com/user-attachments/assets/9050409e-20c3-4cee-87c4-4a3c031e0c1c" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
