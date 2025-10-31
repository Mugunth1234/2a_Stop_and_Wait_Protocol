# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

Client.py
```
import socket
import time

client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)

while True:
    msg = input("Enter a message (or type 'exit' to quit): ")
    client.send(msg.encode())

    if msg.lower() == 'exit':
        print("Connection closed by client")
        client.close()
        break

    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        time.sleep(1)  # Wait 1 second before retrying
        continue


```
Server.py
```
import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")

try:
    conn, addr = server.accept()
    print(f"Connected with {addr}")

    while True:
        data = conn.recv(1024).decode()
        if not data:
            break

        print(f"Received: {data}")
        conn.send("ACK".encode())

        if data.lower() == 'exit':
            print("Connection closed by client")
            break

except KeyboardInterrupt:
    print("\nServer stopped manually")

finally:
    conn.close()
    server.close()
    print("Server socket closed")
```
## OUTPUT
<img width="1915" height="1133" alt="image" src="https://github.com/user-attachments/assets/cbf75376-c93b-4742-a5c9-94657d0e1d31" />



## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
