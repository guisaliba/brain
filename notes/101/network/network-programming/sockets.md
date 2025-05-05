## what is a socket?
a socket is a way to speak to other programs using standard Unix file descriptors.
when Unix programs do any sort of I/O (input/output), what they are really doing is reading from a file and writing back to a file **descriptor**.
a file descriptor is just an integer associate with an open file. the catch is: this open file can be **anything**, from a network connection, a FIFO, a pipe, a terminal, a real on-the-disk file or anything else.
so, everything in Unix is a file. really. when a program communicates with another program over the Internet, that's happening through a file descriptor.

## a little on file descriptors
