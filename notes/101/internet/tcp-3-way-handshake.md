## what is it?
the three way handshake (3-way-handshake) is a mechanism of the TCP protocol for establishing TCP connections between two processes. this mechanism has its foundations based on **flags** and a  **client/server** architecture.

## flags
there are two possible flags for this mechanism:
1. ACK -> Acknowledgment
2. SYN -> Synchronize
flags are nonetheless **bits** in a TCP packet, two bits for example can represent either an ACK flag or a SYN flag. let's pretend our server received a packet and these two bits are **10**. this means that this packet has the ACK flag on it. if our server responds with another packet and these bits are **11** then there is an SYN/ACK flag on it.

TCP has more flags than these two, but for the three way handshake we'll focus on them.

## the handshake
a TCP connection is often established on three steps:
1. the client sends a packet with a SYN flag on it;
2. the server responds a packet with a SYN/ACK flag;
3. client responds back with an ACK flag.

diving deep into that, we can translate these steps in a conversation between these two:
- **Client**: hey, server! i'm sending a message with sequence number 100 (SEQ = 100). can you synchronize (SYN) it please?
	**Client ---> SYN ---> Server** 
-  **Server**: yes, of course! (ACK) please synchronize the message 200 i'm sending you back (SEQ = 200) and you can also proceed with message 101 (SEQ = 101).
	**Client <--- SYN/ACK <--- Server**
- **Client**: ok, i received message 200 (ACK) and as you've told me, i am now sending message 101 (SEQ = 101)
	**Client ---> ACK ---> Server**

with this conversation completed once, they start exchanging packets based on the sequence number (SEQ), which main goal is to enumerate each one's packets amidst this process.

![[image.jpg]]

#network #protocols