# Introduction

## General idea

- **Layers**: Whole proccess of communication between apps is abstracted through layers.
- **Communication**: Every layer communicates with its higher or lower layers in a predefined way.
- **Protocols**: One layer can have more different implementations (protocols).
- **Sublayers**: One layer or implementation can have more sublayers (usually two).
- **Messages**: Consisted of **header** (control data), and **body** (data that is being transferred).

## OSI

- **7 layers**:
    - **Application layer**: Data exchange between apps (HTTP, telnet, email, ...).
    - **Presentation layer**: For converting data (formating, encryption, compression) to for example JPEG, ASCII, MPEG, ...
    - **Session layer**: Creating, controlling, and destructing sessions between apps, for synchronization.
    - **Transport layer**: Communication service "end-to-end", guarantees package order.
    - **Network layer**:
        - **Addressing**: Unique addresses in whole network, headers in this layer contain source and destination s which do not change.
        - **Routing**: Message forwarding from source to destination.
        - **Routers**: Devices that conduct routing L3 packages in network.
    - **Data link layer**:
        - **MAC**: *Media Access Control*, access to physical medium.
        - **MAC Address**: In the case of medium being shared (more than two participants), headers in this layer contain source and destination MAC address which change after every router, between routers they stay the same.
        - **Trailer**: Trailer is added at the end of the message for error detection.
        - **Frame**: A message in the L2 layer.
        - **Switch**: Devices that forward frames.
    - **Physical layer**: Serial transmission of bits by converting them in to electromagnetic waves with modulation (voltage level, wave length) and transmitted through copper wires, optical fibers, microwaves, etc.

## TCP/IP

- **5 layers**: Session and presentation layer are merged in to the application layer.
- **TCP**: *Transmission Control Protocol*, implementation for L4, transport layer.
- **IP**: *Internet Protocol*, implementation for L3, network layer.

## Vertical data transfer

- **Encapsulation**: Done when transfering data from higher to lower level by adding headers on the start, and sometimes trailers on the end of the message. Entire message is sent as data to the lower level (ignoring structure).
- **Decapsulation**: From lower to higher layer, removing current header, and forwarding the data part of the message to the higher layer.
- **Multiplexing**: From higher to lower layer, messages from different protocols of the higher layer are being labeled in the header of the lower layer.
- **Demutliplexing**: From lower to higher layer, recognising the protocol of the higher layer based on the header of the lower layer.

## Today's computer networks

- **LAN**: *Local Area Network*, usually L2 devices.
- **WAN**: *Wide Area Network*, mostly L3 devices.
- **L2 protocols**: Ethernet, Wireless, MPLS (FrameRelay, ATM, SDH).
- **L3 protocols**: IP, IPv6.
- **Internet**: Multiple different networks connected in to a single unique network.
- **ISP**: *Internet Service Provider*.
- **IXP**: *Internet Exchange Point*.

## Data flow

- **Throughput**: Data transmission speed.
- **Bandwidth**: Connection capacity, maximal flow. 
- **bps**: kbps, Mbps, Gbps, Tbps, measurment units.
- **Delay**: Time of transmission of a whole package between two points in a network.
- **RTT**: *Round Trip Time*, time it takes to recieve a package back after it's being sent.
- **BER**: *Bit Error Rate*, in how many transmitted bits does the statistical error happen.
- **Package loss**: Given in percentages (%), happens due to network congestion.

# Data link layer

## General

- **Horizontal communication**: Communicates with L2 layer on the other device by transfering frames through physical medium.
- **Functions**:
    - **Framing**: Forming frames with defined format of headers.
    - **MAC**
    - **Error detection**: With optional error correction.
    - **Reliability**: Receiving confirmation.
- **Implementation**:
    - **NIC**: *Network Interface Card*.
    - **Hardware implementation**: Fast processing without interrupting CPU.
    - **Physical medium connection**: Tightly connected to the physical medium, physical implementation depends on it and topology.

## Topology

- **Point-to-point**: Direct link from user to user.
- **Ring topology**: Packages circle in one direction or both.
- **Bus topology**: "Battle" for accessing equally shared medium.
- **Star topology**: Central device for intercommunication.
- **Wireless**: Star + Bus topology, one device controls communication, equally shared medium. 

## MAC

- **Broadcast**: Shared medium, all users "see" all packages.
- **Collision**: When more users send their packages in the same time.
- **MAC Protocols**: They define the way of distributed agreement with many users around accessing and sharing the medium.
- **Medium sharing**:
    - **Channel Partitioning**: Dividing the medium (channel) in to smaller parts (timed, frequency, coded), every user exclusively gets its own part of the channel.
        - **TDMA**: *Time Division Multiple Access*, every user gets its own fixed time slot for sending, by predetermined order. If no packages whole channel is left unused.
        - **FDMA**: *Frequency Division Multiple Access*, every user gets its own fixed frequency for sending, packages can be sent parallelly. Unassigned frequencies are left unused.
    - **Taking Turns**: Every user waits, by determined algorithm, to get permission for sending.
        - **Polling**: One Master, rest Slaves. Master calls Slave users and gives them permission for sending.
        - **Token Passing**: Control package (token) is being forwarded around the ring, and through token users are being coordinated in which order to send the packages. Complex implementation, only for ring topologies.
    - **Random Access**: Everyone can send whenever it has a package, so everyone has benefits of the whole medium, required collision handling.
        - **Pure ALOHA**: Everyone can send in every moment. In case of collision packages are being retransmitted again with delay of random amount of time.
        - **Slotted ALOHA**: Packages are being sent only in predefined time intervals (slots). Users must be synchronized. Collision happens in case of more packages are being sent in the same slot, then the packages are being sent again in some next slot with some determined probability (p).
- **CSMA**
- **CSMA/CD**