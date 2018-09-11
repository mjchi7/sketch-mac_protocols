# sketch-mac_protocols
Sketch book for MAC protocols relevant topics

# Token Ring (ref: https://en.wikipedia.org/wiki/Token_ring)
## Operation
1. Connected in a ring topology (where every devices are connected to either side of other devices, forming a ring pattern)
2. An empty "token" frame circulates the ring.
3. Node that have message to send will get hold of the frame and insert data into the frame and set "token" field to 1.
4. The frame will then be passed to neighbors.
5. Node which is the intended receiver will receive and copy the message inside the frame and set "token" field to 0. 
6. When the node that put the message into the frame get back the frame with "token" field as 0, it knows the intended node has received the message. 
7. The node then change the "token" field back to 1 and remove the message in it.
8. The empty frame will then be pass around again.

### Advantages
- Guaranteed 0 collisions.

### Disadvantages
- Throughput suffers when more nodes are being added.
- Network-wide synchronization needed.


# Ethernet (ref: https://en.wikipedia.org/wiki/Ethernet)
## Operation


## Mordern Ethernet
- Nodes are all connected to switch instead.
- In this manner, collision only happens if node and switch communicating with each other at the same time, and the collision is limited to that link only.
- GIGABIT Ethernet allows full duplex communication between node and switch, therefore ethernet is COLLISION FREE



# Carrier Sense Multiple Access/Collision Detection (CSMA/CD) v.s. Carrier Sense Multiple Access/Collision Avoidance (CSMA/CA)
## Similarities
- Both sense channel before transmitting

## Difference
### CSMA/CD 
- After sending packet, it will continue to sense the channel to **detect** for collision (by comparing data transmitted and data received on the same channel)
- Reduce the recovery time of collision (CD will abruptly stop transmission; contrast to CSMA only where transmission will be allowed to finish)
- Suffers from hidden node problem (consider node like A-B-C. If A and C is transmitting concurrently to B, node A cannot detect collision at the B-C side and node C cannot detect the collision at the A-B side.)
- Example: Ethernet

### CSMA/CA
- After sending packet, it will **not** sense the channel to detect for collision, instead it relies on receiver to send an ACK frame back for acknowledgement. If ACK not receive, it assume collision occured.
- Reduce the possibility of collision.
- The collision avoidance is achieved by hand-shaking protocol (RTS/CTS) (Optional) to "secure" a channel, whereas CSMA/CD do not do that.
- Example: IEEE 802.11 WiFi

# Pure Aloha (https://www.cse.iitk.ac.in/users/dheeraj/cs425/lec04.html)
- When node has data to send, just send!
- In a finite amount of time if acknowledge is not received, collision occured! and retry.

# 802.11 MAC (Distributed Coordination Function (DCF) v.s. Point Coordination Function (PCF)
https://en.wikipedia.org/wiki/IEEE_802.11e-2005
