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
