## what is a socket?
a socket is a way to speak to other programs using standard Unix file descriptors.
when Unix programs do any sort of I/O (input/output), what they are really doing is reading from a file and writing back to a file **descriptor**.
a file descriptor is just an integer associated with an open file. the catch is: this open file can be **anything**, from a network connection, a FIFO, a pipe, a terminal, a real on-the-disk file or anything else.
so, everything in Unix is a file. really. when a program communicates with another program over the Internet, that's happening through a file descriptor.
where do we get this file descriptor for a network communication? through making a call to the `socket()` system routine. it returns the socket descriptor, and communication is allowed through it using `send()` and `recv()` socket calls.

so, if a socket descriptor is nothing but a file descriptor, why not use the normal `read()` and `write()` syscalls to communicate through the socket? well, that's possible, but `send()` and `recv()` were made for that job. they are just better to use.

## a little on file descriptors
as the name says, a file descriptor **describes** a file. when you open a file, the OS creates an entry to represent that file and store the information about that opened file.
then, an integer is assigned to that open file, representing it uniquely.
so if there are 100 files opened in your OS, there will be 100 entries in OS (living somewhere in the kernel). these entries are represented each by an integer (...100, 101, 102...).
if your process opens 10 files then your Process Table will have 10 entries for file descriptors. same happens when you open a network socket, it is also represented by an integer and it is called Socket Descriptor.

## internet sockets
there are plenty of Internet sockets, but we'll address only two of them: **Stream Sockets** and **Datagram Sockets**, although Raw Sockets are really powerful too (check on it later).
Stream Sockets are also referred to as `SOCK_STREAM` and Datagram Sockets as `SOCK_DGRAM`, the latter is called sometimes as "connectionless sockets".

### stream sockets
stream sockets are a reliable two-way **connected** communication streams. if you output two items "1" and "2" in this order, they will arrive at that same order at the opposite end. they are also error-free.
what uses stream sockets? lot of stuff do. web browsers for example use the HTTP protocol which uses stream sockets to get pages.
if you `telnet www.google.com 80` (which will connect to Google's IP at port 80) and type `GET / HTTP/1.1` an hit `return` twice, it will spit the HTML of that page `/`  back to you.
stream sockets use TCP protocol to achieve such high level of data transmission quality. TCP ensures data arrives sequentially and error-free.

### datagram sockets
also called connectionless. if you send a datagram, it may arrive, but **out of order**. datagram sockets do not use TCP, they use the "User Datagram Protocol", or UDP.
you don't have to maintain an open connection as you do with stream sockets, hence connectionless. 
just build a packet, put an IP header on it with destination info and dispatch it. no connection needed.
they are used when a few dropped packets are not the end of the universe. multiplayer games, streaming audio, video and other services make use of datagram sockets.

## data encapsulation (network theory)
basically, data encapsulation is: a packet is born, this packet gets wrapped (encapsulated) in a header by the first protocol (e.g.: TFTP), then the whole thing is encapsulated again by the next protocol (e.g.: UDP), then again by the next (IP) then by the final protocol on the physical (hardware) layer (e.g.: Ethernet).
when another computer receives this packet, it starts to unwrap all of it. first the hardware strips the Ethernet header, then the kernel strips the IP and UDP headers, the TFTP program strips the TFTP, and finally we have the data!

that's all. visualizing it should be something like:

![[Pasted image 20250504231230.webp]]