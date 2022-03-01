Homework

Index：

[TOC]

## Homework 1

### Question 1：Chapter 1  Problem 2

Equation 1.1 gives a formula for the end-to-end delay of sending one packet of length L over N links of transmission rate R. Generalize this formula for sending P such packets back-to-back over the N links. 

analysis：

- According to the topic, we' ve all ready known d(the end-to-end) = NL/R
- And when the first packet has reached the destination, the second packet has been stored in the last  router.
- And when the time NL/R+L/R, the second packet has reached the destination, and so on.

 answer:    NL/R+(P-1)L/R=(N+P-1)L/R



### Question 2：Chapter 1 Problem 3

Consider an application that transmits data at a steady rate (for example, the sender generates an N-bit unit of data every k time units, where k is small and fixed). Also, when such an application starts, it will continue running for a relatively long period of time. Answer the following questions, briefly justifying your answer:
a. Would a packet-switched network or a circuit-switched network be more appropriate for this application? Why?
b. Suppose that a packet-switched network is used and the only traffic in this network comes from such applications as described above. Furthermore, assume that the sum of the application data rates is less than the capacities of each and every link. Is some form of congestion control needed? Why?

analysis：

- For question a, according to the topic, we' ve already known that we need to let the application transmit data at a steady rate and continue running for a long time. Then here is no spare time , if we choose the packet-switched network, it would increase group management overhead, such as delay.
- For question b, according to the topic, we' ve already known that the sum of the application data rates is less than the capacities of each and every link. Then there is no such a situation as congestion and queues.

 answer：

- a. Circuit-switched network. Applications require a continuous transmission rate, which means that the line have no spare time. The transmission rate is fixed, so it is very convenient to reserve a certain rate of network, and won't cause the situation as insufficient speed or waste. If packet-switched networks are used, packet management costs will be increased.
- b.No. When the sum of the application data rates is less than the capacities of each and every link, congestion and queues won't happen, so there is no need to set the form of congestion control.



### Question 3：Chapter 1 Problem 4

Consider the circuit-switched network in Figure 1.13 . Recall that there are 4 circuits on each link. Label the four switches A, B, C, and D, going in the clockwise direction.
a. What is the maximum number of simultaneous connections that can be in progress at any one time in this network?
b. Suppose that all connections are between switches A and C. What is the maximum number of simultaneous connections that can be in progress?
c. Suppose we want to make four connections between switches A and C, and another four connections between switches B and D. Can we route these calls through the four links to accommodate all eight ­connections?

analysis：

- For question a, due to the fact that every two routers can be established 4 connections, so there are 16 connections in total.
- For question b, according to question a, we've already know that every two routers can be established 4 connections. But we have to ensure that all connections are between switches A and C, then only A-B-C and A-D-C satisfy, totally 8 connections.
- For question c, there are 4 connections between switches A and C and 4 between B and D, in the while we have to route these calls through the four links to accommodate all eight ­connections. Then the 4 connections between A and C can be divided into two A-B-C and two A-D-C, the 4 connections between B and D can be divided into two B-C-D and two B-A-D.

 answer：

- a. 16
- b. 8 (4 A-B-C; 4 A-D-C)
- c. Yes.  The 4 connections between A and C can be divided into two A-B-C and two A-D-C, the 4 connections between B and D can be divided into two B-C-D and two B-A-D.



## Homework 2

### Question 1: Chapter 2 Problem 6

Obtain the HTTP/1.1 specification (RFC 2616). Answer the following questions:

a. Explain the mechanism used for signaling between the client and server to indicate that a persistent connection is being closed. Can the client, the server, or both signal the close of a connection?

b. What encryption services are provided by HTTP?

c. Can a client open three or more simultaneous connections with a given server?

d. Either a server or a client may close a transport connection between them if either one detects the connection has been idle for some time. Is it possible that one side starts closing a connection while the other side is transmitting data via this connection? Explain.

answer:

a. Either the client or the server can indicate to the other that it is going to close the persistent connection. It does so by including the connection-token "close" in the Connection-header field of the http request.

b. HTTP doesn't provide any encryption services.

c. For clients that use persistent connections should limit the number of simultaneous connections that they maintain to a given server. A single-user client shouldn't maintain more than 2 connections with any server.

d. Yes, it's possible. A client might have started to send a new request at the same time that the server has decided to close the idle connection. From the server's point of view, the connection is being closed while it was idle, but from the client's point of view, a request is in progress.



### Question 2: Chapter 2 Problem 12

Write a simple TCP program for a server that accepts lines of input from a client and prints the lines onto the server’s standard output. (You can do this by modifying the TCPServer.py program in the text.) Compile and execute your program. On any other machine that contains a Web browser, set the proxy server in the browser to the host that is running your server program; also configure the port number appropriately. Your browser should now send its GET request messages to your server, and your server should display the messages on its standard output. Use this platform to determine whether your browser generates conditional GET messages for objects that are locally cached.

answer：

```python
from socket import *
import threading
def Accept(ConnectionSocket, Addr):
	Message = ConnectionSocket.recv(1024).decode('utf-8', 'ignore')
	print(Message)
	ConnectionSocket.send('haha'.encode('utf-8', 'ignore')) 
	ConnectionSocket.close()

ServerPort = 10000
ServerSocket = socket(AF_INET, SOCK_STREAM) 
ServerSocket.bind(('',ServerPort))
ServerSocket.listen()
print('listening...')
while 1:
	ConnectionSocket, Addr = ServerSocket.accept() 
	t = threading.Thread(target=Accept, args=(ConnectionSocket, Addr))
	t.start()

```

