# 0x361 Network and Transport

- [1. Network Layer (3)](#1-network-layer-3)
    - [1.1. IP](#11-ip)
    - [1.2. ICMP](#12-icmp)
        - [1.2.1. command](#121-command)
- [2. Transport Layer (4)](#2-transport-layer-4)
    - [UDP](#udp)
    - [TCP](#tcp)
- [3. Session Layer (5)](#3-session-layer-5)
- [4. Presentation Layer (6)](#4-presentation-layer-6)
    - [4.1. XDR](#41-xdr)
- [Reference](#reference)

## 1. Network Layer (3)
Network layer provides logical communication between hosts. A packet in the network layer is referred to as a *datagram*

### 1.1. IP
The IP service model is a best-effort delivery service: it does not guarantee the delivery of the packet, therefore it is a unreliable service.

### 1.2. ICMP

#### 1.2.1. command

- *tcpdump -nni en0 icmp*: filter icmp packets

## 2. Transport Layer (4)
Transport layer provides logical communication between processes. A packet in the transport layer is refered to as a **segment**

### UDP
unreliable, connectionless service

UDP socket is identified by a two-tuple (dest IP, dest port)

### TCP
reliable, connection-oriented service

TCP socket is identified by a four-tuple (src IP, src port, dest IP, dest port)

## 3. Session Layer (5)

## 4. Presentation Layer (6)

### 4.1. XDR

*   external data representation
*   a standard data serialization format

## Reference
[1] Kurose, James F. Computer networking: A top-down approach featuring the internet, 3/E. Pearson Education India, 2005.