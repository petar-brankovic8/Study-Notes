Author: **Petar Brankovic**  
*School of Electrical Engineering* | **ETF**  
Class: **Computer Networks 1**

# Table of Contents

- [Network models](#network-models)
  - [General idea](#general-idea)
  - [OSI](#osi)
  - [TCP/IP](#tcpip)
  - [Vertical data transfer](#vertical-data-transfer)
  - [Today's computer networks](#todays-computer-networks)
  - [Data flow](#data-flow)
- [Data link layer](#data-link-layer)
  - [General](#general)
  - [MAC](#mac)
  - [Ethernet](#ethernet)
  - [L2 Devices](#l2-devices)
  - [Spanning-Tree Protocol](#spanning-tree-protocol)
  - [Virtual LAN](#virtual-lan)
  - [Wireless LAN](#wireless-lan)
- [Network layer](#network-layer)
    - [General](#general-1)
    - [Internet Protocol - IP](#internet-protocol---ip)
    - [Routing](#routing)
    - [Routing Protocols](#routing-protocols)
    - [Distance Vector](#distance-vector)
    - [Link-State](#link-state)
    - [OSPF](#ospf)
- [Transport layer](#transport-layer)
    - [General](#general-2)
    - [TCP](#tcp)
- [Application layer](#application-layer)
    - [Protocols](#protocols)
    - [DNS](#dns)
- [Additional protocols](#additional-protocols)
    - [DHCP, NAT, ACL](#dhcp-nat-acl)
    - [IPv6](#ipv6)

# Network models

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
    - **Transport layer**: Communication service "end-to-end", guarantees packet order.
    - **Network layer**:
        - **Addressing**: Unique addresses in whole network.
        - **Routing**: Message forwarding from source to destination.
        - **Routers**: Devices that conduct routing L3 packets in network.
    - **Data link layer**:
        - **MAC**: *Media Access Control*, access to physical medium.
        - **Trailer**: Trailer is added at the end of the message for error detection.
        - **Frame**: A message in the L2 layer.
        - **Switch**: Devices that forwards frames.
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
- **Bandwidth**: Connection capacity, maximum throughput. 
- **bps**: kbps, Mbps, Gbps, Tbps, measurment units.
- **Delay**: Time of transmission of a whole packet between two points in a network.
- **RTT**: *Round Trip Time*, time it takes to recieve a packet back after it's being sent.
- **BER**: *Bit Error Rate*, in how many transmitted bits does the statistical error happen.
- **Packet loss**: Given in percentages (%), happens due to network congestion.

# Data Link layer

## General

- **Horizontal communication**: Communicates with L2 layer on the other device by transfering frames through physical medium.
- **Functions**:
    - **Framing**: Forming frames with defined format of headers.
    - **MAC**
    - **Error detection**: With optional error correction.
    - **Reliability**: Receiving confirmation that the packet is received (optional).
- **Implementation**:
    - **NIC**: *Network Interface Card*.
    - **Hardware implementation**: Fast processing without interrupting CPU.
    - **Physical medium connection**: Tightly connected to the physical medium, physical implementation depends on it and topology.

- **Topology**
    - **Point-to-point**: Direct link from user to user.
    - **Ring topology**: Packets circle in one direction or both.
    - **Bus topology**: "Battle" for accessing equally shared medium.
    - **Star topology**: Central device for intercommunication.
    - **Wireless**: Star + Bus topology, one device controls communication, equally shared medium. 

## MAC

- **Broadcast**: Shared medium, all users "see" all packets.
- **Collision**: When more users send their packets in the medium at the same time.
- **MAC Protocols**: They define the way of distributed agreement with many users around accessing and sharing the medium.
- **Medium sharing**:
    - **Channel Partitioning**: Dividing the medium (channel) in to smaller parts (timed, frequency, coded), every user exclusively gets its own part of the channel.
        - **TDMA**: *Time Division Multiple Access*, every user gets its own fixed time slot for sending, by predetermined order. If no packets, whole channel is left unused.
        - **FDMA**: *Frequency Division Multiple Access*, every user gets its own fixed frequency for sending, packets can be sent parallelly. Unassigned frequencies are left unused.
    - **Taking Turns**: Every user waits, by determined algorithm, to get permission for sending.
        - **Polling**: One Master, rest Slaves. Master calls Slave users and gives them permission for sending.
        - **Token Passing**: Control packet (token) is being forwarded around the ring, and through token, users are being coordinated in which order to send the packets. Complex implementation, only for ring topologies.
    - **Random Access**: Everyone can send whenever it has a packet, so everyone has benefits of the whole medium, required collision handling.
        - **Pure ALOHA**: Everyone can send in every moment. In case of collision packets are being retransmitted again with a delay of random amount of time.
        - **Slotted ALOHA**: Packets are being sent only in predefined time intervals (slots). Users must be synchronized. Collision happens in case of more packets are being sent in the same slot, then the packets are being sent again in some next slot with some determined probability (p).
- **CSMA**: *Carrier Sense Multiple Access*, all devices are "listening" for the activity on the medium, if the medium is busy they wait, if it's free they send. Possible collision when more devices start sending the packets in close time moments while the signal still hasn't got to them because of its propagation speed.
- **CSMA/CD**: *CSMA/Collision Detection*. Collision detection is done by listening to the signals from medium and sending in the same time and then checking if they are the same.

## Ethernet

- **2 Sublayers**:
    - **LLC**: *Logical Link Control*, for multiplexing and encapsulating protocol of the higher layer.
    - **MAC**
- **CSMA/CD**:
    - **Detection**: Devices that receive that packet must detect the collision so that they can reject the invalid packet, and the devices that send also need to detect it because they must send it again, and they can detect it only while they are sending it.
    - **JAM frame**: Collisions can even happen only on one bit, so for the non-sending devices to detect it, the sending device must send a JAM signal, consisting of 32 alternating bits of zeros and ones, indicating that there was a collision.
    - **Detection condition**: For the sender to detect the collision, in the worst case the packet will travel to the furthest device in the network and in that moment that device will also start sending the packet, then moment after it detects the collision and starts sending the JAM signal. That JAM signal must reach the original sender before it got finished sending its original packet so it can know that it needs to send it again. So the packet must be large enough that it is being sent longer than it takes for the signal to go to the furthest place and come back (t_out > 2t_p).
    - **bit-time**: Time it takes for one bit to get out on network, depends on bandwidth (t_b = 1 / B). Used for calculating time it takes for a whole frame to get out on a network (t_out = L \* t_b = L / B).
    - **Repeater**: Receives signals from one segment of coaxial cable (maximal length 500m), recognizes bits (zeros and ones), sends new regenerated signals on the other segment. Increases maximal length of a network. Limitation is 4 repeaters maximum in a row.
    - **Calculation**: 
        - **Maximum length**: Two furthest points in a network: 2500m (A-500m-R1-500m-R2-500m-R3-500m-R4-500m-B). 
        - **Propagation time**: Signal is travelling through copper cable around 2/3 of speed of light (2\*10^8m/s). Time of propagation through one segment is t_p = 500m / 2\*10^8m/s = 2.5 micro seconds. 
        - **Repeater delay**: t_r = 3 micro seconds. 
        - **Maxium delay**: In both directions t_d(max) = 2*(5\*t_p + 4\*t_r) =  49 micro seconds.
        - **Slot-time**: Time it takes for a frame to get out in network (slot-time) t_s = t_out > t_d(max) = 49 micro seconds.
        - **Bandwidth**: B = 10Mbps (First ethernet, later it goes faster so its maximum length is lower).
        - **Minimum frame length**: L_min = B / t_s = 10Mbps / 49 micro seconds = 490b.
        - **Frame length**: The used frame length is L = 512b = 64B.
    - **Algorithm**
    ```mermaid
    flowchart TD
    S[Start CSMA/CD] --> PF[Prepare the frame]
    PF --> MF{Medium free?}
    MF -->|No| PF
    MF -->|Yes| SOB[Send one bit]
    SOB --> C[Collision?]
    FS -->|Yes| SC[Sending succesfull]
    FS -->|NO| SOB
    C -->|No| FS{Finished sending?}
    C -->|Yes| SJ[Send JAM]
    SJ --> NPP[N = N + 1]
    NPP --> N16{N = 16?}
    N16 -->|Yes| SU[Sending unsuccesfull]
    N16 -->|No| KRAND[K = random number from 0 to 2^N-1]
    KRAND --> W[Wait K*t_s]
    W --> PF
    ```
- **Addressing**:
    - **MAC Adress**: Physically written in ROM of network cards (*Burned-In Address - BIA*), globally unique. It has 6 bytes, 3 for *Organizational Unique Identifier* (OUI), 3 for identification of produced card.
    - **Unicast address**: Network address that identifies a single, unique device. Used when sending to that one specific device, not to multiple devices.
    - **Broadcast address**: Used when addressing all devices on network. Has all ones (FFFF.FFFF.FFFF).
    - **Multicast address**: Used when addressing only specific devices.
- **Ethernet Frame Format**: Preamble (7B) - SFD (1B) - Dst (6B) - Src (6B) - T/L (2B) - Data (46B-1500B) - FCS (4B)
    - **Preamble**: Used for synchronization of oscilators on receiving devices, it consists of 7 bytes of alternating zeros and ones.
    - **SFD**: *Start of Frame Delimiter*, 1 byte - 10101011, last two ones indicate start of the "real" ethernet frame.
    - **Destination**: Destination MAC address, device for whom the packet is sent.
    - **Source**: Source MAC address, device that sent the packet.
    - **Type / Length**: 
        - **Type**: Identification of protocol of L3, for multiplexing and demultiplexing (for Ethernet II)
        - **Length**: Length of data field, max 1500B (for IEEE 802.3)
        - **Type/Length**: Values until 1500 represent Length, values until 1536 represent Type (for merged IEEE 802.3x).
    - **FCS**: *Frame Check Sequence*, used for checking if there was some mistake using Cyclic Redundancy Check (CRC).
- **Interframe gap**: Minimal gap between two frames - 96\*t_b (for 10Mbps - 9.6 micro seconds). Reason is that frames cannot be attached, electronics in network card needs to change to state of receiving, otherwise it could miss the start of the next frame.

## L2 Devices

- **Collision domain**: All devices connected to a shared medium. Larger collision domain leads to higher probabilities of collision and worse performance of the network.
- **Bridge**: Splits LAN network in two collision domains.
    - **Port**: Every port belongs to different collision domain.
    - **Transparet bridging**: Hosts do not know of existence of bridges, they do not need any special configuration when connecting to them.
    - **Bridge Table**: It holds MAC address of the host paired with port ID.
    - **5 bridging processes**:
        - **Forwarding**: Happens when destination and source device are on different segments. Bridge takes frame on one port, looks at its destination MAC address in bridge table, and if the output port is not the same as input port, it forwards the frame.
        - **Filtering**: Happens when destination and source device are on the same segment. Bridge takes frame on one port, and if the port of the destination MAC address is same as input port it filters it out.
        - **Learning**: Bridge table is empty when the bridge turns on. When it takes a frame, it looks at its source MAC address and writes and pairs it with input port in the bridge table.
        - **Flooding**: Happens when destination MAC address isn't in a bridge table. After it fails to find a destination MAC address, it sends the frame to all other bridge ports.
        - **Aging**: Every row in a bridge table has a timer. If there isn't traffic from a certain MAC address for that specified timer time (usually 2min) it gets deleted from the table. It is a protection from filling the whole bridge table, and for updating ports if the device is changed to another one.
- **Hub**: Central device in ring topology. Used to localize network failures from often cable damaging. It is a multi-port repeater, receives on one port and sends regenerated signal on all others.
- **Switch**: Multi-port bridge and a smart hub.
    - **Half Duplex**: Segment between switch and device is a shared medium, collision possible if device and switch start sending at the same time.
    - **Full Duplex**: UTP and optic cables have separate receive and transmit medium, so no collision possible (used today).
    - **Frame loading and forwarding**:
        - **Store and Forward**: Switch receives the whole frame, checks FCS, and forwards it to output port.
        - **Fragment Free**: Switch starts forwarding after receiving first 64 bytes (when working with hubs to prevent collision).
        - **Cut-Through (Fast Forward)**: Switch start forwarding after receiving destination MAC address (only 6 bytes).
    - **Port bandwidth**:
        - **Auto-negotiation**: Switch and connected device automatically establish connection on fastest supported bandwidth (Switch label: 10/100/1000BASE-T).
        - **Simmetric forwarding**: When input port that receives the frame has the same bandwidth as output port that forwards the frame.
        - **Asimmetric forwarding**: When input and output port have different bandwidths. Store-and-Forward must be used.

## Spanning-Tree Protocol

- **Ethernet limitations**:
    - **Scalability**: Solution is bridges and switches.
    - **Bus topology resistance**: Solution is star topology (acyclic) with hubs and switches.
    - **Star topology resistance (switch failure)**: Solution is redundant topology to remove single point of failure (two switches doing the same thing, in case one fails, cyclic topology).
- **Loop problems**: In cyclic topologies.
    - **Duplicated received packets**: When flooding, a packet is sent twice to the receiver by PC1-SW1-SW2-PC2 and PC1-SW1-SW3-SW2-PC2.
    - **Broadcast storm**: When broadcast frame is sent SW1, SW2, SW3 will constantly receive and send packets to one another creating an infinite loop.
    - **Bridge table unstability**: When PC1 is sending broadcast frame, two same frames from PC1 will come to the switch from different ports, changing its port bridge table value.
- **Spanning-Tree Protocol**: Solution for loops, by removing them, by blocking certain ports in switches (establishing "spanning tree" inside graph topology).
- **Parameters**:
    - **Bridge/Switch Identification (Bridge ID)**: Two fields (8B): Bridge Priority (2B), MAC (6B).
    - **Port Cost**: Integer value assigned to the port. Inversly proportional to port bandwidth.
    - **Path Cost**: Sum of port costs from the source to the destination. Determines the path metric for deciding which path is better. Best path has the least cost.
- **BPDU**: *Bridge Protocol Data Unit*, It is a STP message which switches use to communicate with each other. It is encapsulated inside of Ethernet frame. STP is an L3 protocol. It holds Root ID (8B), Path Cost (4B), Bridge ID (8B).
    - **Configuration BPDU**: Sent from Root switch to configure the network properly. Has a *Topology Change Notification* (TCN) flag that signals to switches that there has come to topology change in network, if the flag is turned on it shortens the aging timer for bridge table of the switch.
    - **TCN BPDU**: Sent by switch that detects the topology change to the Root switch to inform him.
- **STP process**:
    - **Root Switch Selection**:
        - **Root switch**: Switch with smallest Bridge ID.
        - **Initialization**: When turned on, switches do not have information about each other, and they declare themselves as root switch.
        - **Configuration BPDU message**: This message has *Root Bridge ID* field, and when adjacent switches receive this message they compare their Root Bridge ID with the received one, and if the received one is lower, then it is set as the new Root Bridge ID and sent further.
    - **Root port selection**:
        - **Root port (RP)**: Port that leads to the "best" path to root.
        - **Configuration BPDU message**: Now only root switch initially sends these messages that contain Path Cost, and when every switch receives them and adds the Port Cost to the Path Cost and sends it further to the rest of the switches. 
        - **Selecting**: The port that received the message with smallest Path Cost is set as the Root port. Only one port in switch can be a root port. If more ports receive the same Path Cost value then the one with smaller Bridge ID is selected. If there is a parallel connection between two switches, then the port with smaller internal order number is selected.
    - **Designated port selection**:
        - **Designated port (DP)**: If more ports lead to the same segment (for example, hubs). Only one port on the segment can be a designated port. It leads to the "best" path from the segment to the root. 
    - **Blocked port (BP)**: Ports that are not Root or Designated ports are put in the blocking state. They throw away all non-BPDU frames.
- **Stationary state**: Root switch emits Configuration BPDU every 2 seconds (*Hello* timer) that goes only through root and designated ports.
- **STP Convergence**: Adapting to the change of topology or state of STP (removal or addition of links). Transitions from forwarding states to blocking states of ports can happen in the moment, but in order to prevent temporary loops, transitions from from blocking states to forwarding states need to be done carefully by giving time to other switches to converge.
    - **STP Timers**:
        - **Hello timer**: Period of emitting Configuration BPDU message from the Root Bridge - 2 seconds.
        - **Max Age timer**: In case the switch doesen't receive BPDU messages anymore, time of waiting before it initiates a new process of setting up STP topology - 10 \* Hello period.
        - **Forward Delay**: Time of waiting to ensure that all information propagates to all parts of network, by waiting all switches to be setted up properly - 15 seconds.
        - **Synchronization**: Timers must be synchronized on all switches of the network, which is done by sending them in BPDU messages.
    - **STP port states**:
        - **Blocking state**: No frames with data are being forwarded, only BPDU packets are being accepted.
        - **Listening state**: Temporary (transition) state - 15 seconds (Forward Delay timer). No frames with data are being forwarded. BPDU packet start to also being sent through these ports. STP parameters are being calculated. Bridge table aging timer for MAC addresses is being set to 15 seconds so the table would be clear.
        - **Learning state**: Temporary (transition) state - 15 seconds (Forward Delay timer). Frames with data are only being accepted, not forwarded (they are thrown away). Switch begins to learn MAC addresses and form valid bridge table. Used to avoid too much flooding after port activation.
        - **Forwarding state**: All frames are being forwarded in both directions.
- **EtherChannel**: More parallel connections between two switches (devices) merged in one logical connection. Increased bandwidth and resistance to failure of single connection. It doesen't break the STP tree.
- **PortFast**: STP is initally done on all ports, even on those that aren't connected to switches, but to other devices (access ports). When the device is turned on, on that port comes to convergence and it begins its learning and listening to prevent loop creation. Unnecessary. PortFast are configured on access ports so they immediatly go in forwarding state. Problem is it doesen't prevent someone from connecting a switch to that port which may create temporary loops.
- **Security**:
    - **Problem**: Attacker can connect his laptop to two switches from the network, and do switch function with appointed best priority and become the root switch from where he can eavesdrop all communication.
    - **Root Guard**: Forbids receiving BPDU frames with better Bridge ID on that port, which stops a better candidate for root switch to appear on that port.
    - **BPDU Guard**: Used in pair with PortFast on access ports, it disables a port when it receives BPDU frames and activates it back when it stops receiving BPDU frames.
- **Base problems**: Slow convergence - up to 50 seconds. No load-balancing - only one link is used while others are blocked. Unopmtimal traffic paths if Bridge IDs arent set up.
- **Rapid Spanning Tree Protocol (RSTP)**
    - **Link types**:
        - **Edge Type**: Link between switch and end devices (hosts).
        - **Link type**: Link between switches. Can be Point-to-Point (directly connect switches) or Shared (connected through shared medium - hub).
    - **New port states**:
        - **Alternate port**: Blocked port, best port after Root Port. Replacement for Root Port, ready to get Root Port role in case that original one stops receiving BPDU messages with lowest Path Cost.
        - **Backup port**: Special and extremly rare case, when switch is connected to a hub with multiple links. Blocked port, best port after Designated Port and its replacement.
    - **MaxAge**: RSTP uses 3\*Hello interval - 6 seconds.
    - **RSTP Convergence**:
        - **Change in Edge Type link**: RSTP uses PortFast mechanism on Edge Type links.
        - **Change in Link Type Shared link**: RSTP behaves same as STP.
        - **Change in Link Type Point-to-Point link**: Active communication between switches during process of convergence.
            - **New types of BPDU messages**:
                - **Proposal**: BPDU with set Proposal flag.
                - **Agreement**: BPDU that confirms branch in the tree, sent by Root Port.
            - **Process**: Listening state isn't used. Learning state is very short. Fast transition to forwarding state, usually less then 1 second for all switches in the network. Done by proposing new Root Port, if agreed block the old Root Port, continue with adjacent switches.

## Virtual LAN

- **VLAN**: *Virtual Local Area Network*, logically divides physical LAN network on independent logical LAN networks.
- **Configuring VLAN**: Done on switches with software. Ports are paired with matching VLAN. Problem is when devices from same VLAN are on many different switches.
    - **Statically**: Certain ports are dedicated to some VLAN while configurating.
    - **Dynamically**: By some packet parameter, traffic is assigned to certain VLAN.
- **Trunk link**: Shared link for all VLANs.
    - **Access port**: They forward only one VLAN on links.
    - **Trunk port**: On trunk links they forward multiple VLANs (port types must match on both sides of the link).
- **VLAN Frame Tagging**: On trunk links in Ethernet header 4B are added. 3B are for VLANID.
- **PVST**: *Per-VLAN STP*, independent STP execution for different VLANs, more optimal use of physical links.

## Wireless LAN

- **Shared medium**: Only one frequency is used for all devices.
- **Half-duplex**: Only one device can send frames in one moment.
- **CSMA/CA**: *Carrier-Sense Multiple Access/Collision Avoidance*, in wireless, collision cannot be detected because signal losses its power much faster while travelling.
- **Service Set**: Group of connected devices - WLAN network.
- **Types of WLAN**:
    - **IBSS**: *Independent Basic Service Set*, Ad-hoc regime, no central device, all devices are equal.
    - **BSS**: *Basic Service Set*, has a central device - **Access Point (AP)**, all communication done through AP.
    - **ESS**: *Extended Service Set*, has more APs connected through a switch.
- **WLAN cell**: Range area of a single AP.
- **AP antenna**: Signal reflection from the objects in surrounding space can cause signal distortion. Placing two antennas spaced apart for 1/2 wave length can compensate the distortion.
- **SSID**: *Service Set Identifier*, name of the WLAN network - text of maximum 32 characters.
- **Beacon frames**: Periodically sent by AP. Contains SSID and MAC address of the AP. Network becomes visible for other devices.
- **Connecting to WLAN**:
    1. **Parameter exchange**: Alignment of supported standards, frequencies, bandwidth, ... (Probe Request, Probe Response).
    2. **Authentication**: Authencation Request, Authentication Response.
    3. **Association**: Association Request, Association Response.
- **Communication**: All devices communicate through AP, they cannot directly. They can detect frames from other devices, but they accept only ones from AP. APs are usually connected to a switch from some LAN network, so they must convert Wireless frames to Ethernet frames (*bridging mode*).
- **Integration with LAN/VLAN**: Mapping SSID in to VLAN, all devices connected to the AP are part of that VLAN. If we want more VLANs on one AP, it is possible to have more SSIDs on one AP that are mapped to separate VLANs, and connect AP with switch using trunk link.
- **Power Over Ethernet (POE)**: Special switches can send DC of 12V through UTP cables (they have 4 pairs of twisted copper wires, 2 used for communication, 2 left unused). APs have Ethernet ports, so if it is harder to connect them to power supply (they are usually close to ceiling) they can have an option to get it from UTP cable.
- **WLAN channels**: One channel is one frequency domain that has fixed width (20MHz, 40MHz). Adjacent channels are spaced apart for 5MHz, they overlap. APs support more channel, but work only on one at a time.
- **WLAN area coverage**: If we want to cover a wider area with our WLAN, we can use multiple APs whose cells should overlap so we don't lose signal in between them. Cells that do overlap shouldn't be on overlaping channels to avoid signal interference (at least 20MHz appart). If the signal of one AP goes weak, device automatically switches to other AP with stronger signal.
- **Channel scanning**:
    - **Passive scanning**: Device waits for AP to send beacon frame.
    - **Active scanning**: Device sends special request for available channels - Request Probe packet.
- **Frame format**: Ctrl (2B) - Dur (2B) - Adr1 (6B) - Adr2(6B) - Adr3 (6B) - Seq (2B) - Adr4 (6B) - Data (0-2312B) - FCS (4B)
    - **Frame Control**: Different flags.
    - **Addresses**: Use of address fields depends on use case that is determined by two flags in control field "To DS" and "From DS" (Distribution System).
        - **Source Address (SA)**: Source device.
        - **Transmitter Address (TA)**: Source device or AP.
        - **Receiver Address (RA)**: Destination device or AP.
        - **Destination Address (DA)**: Destination device.
    - **Duration**: Approximation of time during which medium will be taken.
        - **NAV**: *Network Allocation Vector*, value that goes in duration field, depends on frames size and bandwidth. Based on it other devices know when the medium will be free.
- **Carrier Sense**:
    - **Physical**: Listening if the medium is free or taken.
    - **Virtual**: Happens during NAV time, devices do not have to actively listen and check the medium. Reduces activity on device which saves battery.
- **CSMA/CA**:
    - **PCF**: *Point Coordination Function*, one central device (AP) "calls out" other devices and gives them permission for sending.
    - **DCF**: *Distributed Coordination Function*, all devices are equal (including AP), and "fight" for taking medium.
        - **DIFS**: *Distributed Inter Frame Space*, fixed time interval that devices wait before sending their packet when they see that medium is free.
        - **Back-off**: Additionally to DIFS, there is random time interval that is waited before sending the packet after the DIFS passed. This random time is calculated by choosing a random number R (from 0 to CW - *Contention Window*) multiplied by ST (*Slot-Time*). CW is increased exponentionally with number of failed attempts. 
            - **Back-off timer pause**: This timer is being paused when the medium is being taken and when it gets free again DIFS time is waited and back-off timer continues to count down from where it was paused. 
            - **Back-off timer condition**: It is created only when device becomes ready to send when the medium is taken. Otherwise when the medium is free and device becomes ready to send in that moment no back-off timer is being created.
        - **Positive Acknowledgement (ACK)**: Every frame that is succesfully received without collision, must be confirmed. If there was a collision the device that originally sent the frame, won't get the ACK, and sends the frame again. Confirmation is also indirectly forwarded through AP.
        - **Two-Way Handshake**: Transmission in two steps, one device sends the frame with data to the other one, the other one sends ACK back.
        - **Four-Way Handshake**:
            - **RTS**: *Request To Send*, one device requests to send a frame to the other one.
            - **CTS**: *Clear To Send*, the other device approves sending.
            - **Sending**: Sending the frame with data.
            - **Acknowledgement**: Confirming receiving the data.
        - **SIFS**: *Short Inter Frame Space*, short time (shorter than DIFS) of waiting for ACK frame to arrive data frame in two-way handshake, or waiting for CTS, then data, and then ACK frame to arrive after RTS in four-way handshake. All of these times are included in one NAV.
- **Security**: Because of the shared medium all devices can read the packets.
    - **WEP**: *Wired Equivalent Privacy*, hackable and not used anymore.
    - **WPA**: *Wi-Fi Protected Access*, Wi-Fi - community of wireless equipment manufacturers.
    - **WPA 2**: Modernly used.


# Network layer

## General

- **Scalability problem**: If we wanted to cover a whole world with L2 devices and connect them in such a network, which theoretically could be possible, bridge tables of every switch would be overwhelmed and loaded with milions of MAC addresses.
- **Routers**: L3 devices. They connect LAN networks (they represent border between LAN networks). Router ports have L2 layer and MAC addresses that are used in frame header. They view frames on L3 layer and change addresses on L2 layer.
- **Network layer (L3)**:
    - **Topology**: Allows arbitrary topology of connected routers network.
    - **Addressing**: Unique addressing on whole network (globally).
    - **Routing**: Message forwarding from source to destination.
    - **Protocols**: There existed many kinds of network layer protocols, but today only Internet Protocol (IP) is used.

## Internet Protocol - IP

- **Characteristics**:
    - **Connectionless**: There is no establishing active connection from end-to-end. Sender doesen't know if receiver is connected to a network or if he even exists, if the packet made it to the receiver, or if the packet is damaged, if the receiver can even read it, and receiver doesn't know when the packet is going to arrive.
    - **Media Independent**: Doesen't depend on physical medium and protocols on first and second layers. IP is encapsulated in L2 protocols.
    - **Best Effort (Unreliable)**: No guarantee that the packet will arrive at destination.
- **IP packet**: Encapsulates L4 messages.

<table border="1" cellspacing="0" cellpadding="4">
  <tr>
    <th align="center" colspan="8">1. byte</th>
    <th align="center" colspan="8">2. byte</th>
    <th align="center" colspan="8">3. byte</th>
    <th align="center" colspan="8">4. byte</th>
  </tr>
  <tr>
    <td align="center" colspan="4">VERS</td>
    <td align="center" colspan="4">HLEN</td>
    <td align="center" colspan="8">Type of Service</td>
    <td align="center" colspan="16">Total Length</td>
  </tr>
  <tr>
    <td align="center" colspan="16">Identification</td>
    <td align="center" colspan="3">Flags</td>
    <td align="center" colspan="13">Fragment Offset</td>
  </tr>
  <tr>
    <td align="center" colspan="8">Time to Live</td>
    <td align="center" colspan="8">Protocol</td>
    <td align="center" colspan="16">Header Checksum</td>
  </tr>
  <tr>
    <td align="center" colspan="32">Source IP Address</td>
  </tr>
  <tr>
    <td align="center" colspan="32">Destination IP Address</td>
  </tr>
  <tr>
    <td align="center" colspan="24">Options</td>
    <td align="center" colspan="8">Padding</td>
  </tr>
  <tr>
    <td align="center" colspan="32">Data</td>
  </tr>
</table>

- **IP header**:
    - **VERS**: Version. IPv4 - base version, still dominant on Internet. IPv6 - "new" version, uncompatible with IPv4.
    - **HLEN**: Header Length. Calculated in number of words of 4 bytes (usually has value 5).
    - **Total Length**: Whole size of IP packet in bytes, including a header.
    - **Header Checksum**: Error control for header (same as FCS, but just for header of IP).
    - **Protocol**: Identification of L4 protocol (1 - ICMP, 6 - TCP, 17 - UDP, 89 - OSPF).
    - **Type of Service (ToS)**: For defining packet priority depending on which traffic class they belong to. Initially it was *IP Precendece*, now it is modified in DSCP (*DiffServ Code Point*) that uses 6 bits to represent traffic class and packet priority.
    - **Options**: For testing and other certain options.
    - **Padding**: Filling space to the full word of 32 bits.
    - **TTL**: *Time to Live*, usually starts with value 255. Gets decremented in every router it passes through, and when it reaches zero, packet is being thrown away. Prevents infinite loops in case of mistakes in network configuration ("logical" loops).
- **MTU**: *Maximum Transmission Unit*, on L2 layer. Limited size of L2 frame.
- **Fragmentation**: Happens when IP packet is larger than MTU and can't fit in a frame. Solution is dividing one IP packet on more smaller IP packets (fragments).
    - **Identification**: Every packet has a unique ID of 16 bits. All fragments have same ID - they belong to a same IP packet.
    - **Flags**: Control Bits
        - **Flag DF**: *Don't Fragment*, 1 - forbids fragmentation, 0 - allows fragmentation.
        - **Flag MF**: *More Fragment*, 1 - isn't last fragment of the original packet, 0 - represents a last fragment.
    - **Fragment Offset**: Relative position of data based on data of original IP packet. Measured in units of 8 bytes.
    - **Reasembling**: Merging data of all fragments in to original array of data from original IP packet. Done in destination when packet arrives. Has a timer in which if all fragments do not come, the packet is being thrown away. 
- **IP address**: They identify devices. Has length of 4 bytes.
    - **Source IP Address**: Part of IP packet header.
    - **Destination IP Address**: Part of IP packet header.
    - **Dotted Decimal**: Notation for representing IP addresses - decade numbers separated by dot. Example: 147.91.11.21, 192.168.0.11...
    - **Grouping**: IP addresses of devices in a same LAN are grouped in joint network IP address. LAN network on L2 layer is mapped in to IP network on L3 layer. All devices in one LAN have same IP address "prefix" that repsresents that network.
    - **Two parts of IP address**: Address of a network - "left part of the address", "network part". Address of a device in the network - "right part of the address", "host part".
    - **Network address**: Bits with value zero in host part.
    - **Broadcast address**: Bits with value one in host part.
    - **Device address**: Arbitrary values that are left. Potential number of hosts in the network: 2^n-2 (n - number of bits in host part).
- **Classful addressing**: Address where split in classes: A, B, C, D and E. They were determined by starting bits. Classes A, B, and C where for users. D for multicast, E for experimental uses.
    - **Private addresses**: Reserved addresses for isolated use outside of Internet. They can't be seen on Internet, because they are not unique. Classes for users have defined ranges for private addresses (range for C class: 192.168.0.0 - 192.168.255.255).
    - **Other reserved addresses**:
        - **Default route**: From A class - 0.0.0.0
        - **Loopback address**: From A class - 127.0.0.1. Local predefined address on every device.
- **Subneting - Classless**: Classful was unproportional for address part and host port.
    - **Subnetting**: Dividing on smaller parts - subnetworks. Bit part for addressing the host is used for identifying subnetworks. Added new hierachical level.
    - **Host part**: Minimal number of hosts in network is 2. Minimal number of bits for host part is 2 (2^n-2, n=2).
    - **Classless**: Term "network" and "subnetwork" is being equalized, independent of classes.
    - **Mask**: Mask divides address on network part and host part. It is made of 32 bits with leading ones.
        - **Dotted Decimal notation**: In form of IP address, for example 255.255.255.0.
        - **Prefix notation**: "/n" - n is number of ones in a mask, for example "/24".
        - **Mask information**: When address is given with a mask, it also contains information to which network does the unique IP address of a host belong to.
        - **VLSM**: *Variable Length Subnet Mask*, using masks od different lengths in one network.
        - **Supernetting**: Merging more adjacent subnetworks in one larger subnetwork using a common mask.

## Routing

- **Router (gateway)**: L3 communication device.
    - **Working principle**:
        1. **Input interface**: Port on which they receive packages.
        2. **IP address look-up**: Destination IP address that is being looked up.
        3. **Output interface**: Output port that leads to destination determined by destination IP address.
    - **Interface**: Module/Card/Port on router.
        - **Name**: Each interface has a symbolic name (Serial, FastEthernet, GigabitEthernet, ...) and a numeric label (index).
        - **IP address**: Each interface has its own IP address.
        - **MAC address**: For LAN ports.
- **Next-hop**: "Next step on the packets way to destination address". It is IP address of the adjacent routers inteface on the common link or network. 
- **Routing**: Forwarding packets on the next-hop address based on destination (*Destination-based routing*).
    - **Source-based routing**: It is possible to force routing through predefined interfaces (very rare use case).
- **Routing table**: Contains IP address and their assigned next-hop address (address that lead to them).
    - **Route**: Row in routing table (network and next-hop).
    - **End devices routing table**: End devices (like PCs, laptops, servers) also have routing tables.
- **Default gateway**: 
    - **Predefined exit**: Predefined exit of the IP (local) network. 
    - **Routers interface**: Interface on the router that belongs to the subnetwork represents its predefined exit. 
    - **IP communication**: Used for communication between different IP networks - through router. 
    - **Hosts**: All hosts on IP layer must have defined their default gateway in order to communicate outside the local network.
- **Broadcast domain**: Equivalent to collision domain on L2, just on L3. Routers are borders for broadcast domains, like switches for collision domains.
- **Static routes**: Manually configured routes on routers for certain networks. "Use next-hop x.x.x.x for network x.x.x.x/X".
    - **Pros**: Simple, doesen't require extra resources, readable.
    - **Cons**: Changes in network require manual configuration on large number of devices, unscalabale for larger networks.
- **Dynamic routes**: Routers exchange infromations about networks on their own, similar to STP. Defined by routing protocols.
- **Default route**: Predefined route for all networks without their own individual route.
    - **0.0.0.0**: Default route label. Contains mask "/0", which means it contains all networks.
    - **Single exit link**: If there is only one link to the rest of the network, routing table can contain only small amount of routes to certain "internal" networks, and default route for all other networks (including the whole Internet).
    - **No default route**: If routing table doesen't contain route to certain network, and doesen't have default route, packets for that network are being thrown away.
- **Most specific route rule**: If in routing table there are more networks in which a destination can belong to, this rule chooses the smallest network, the one with longest prefix (mask).
- **ARP - Address Resolution Protocol**: Automated MAC address discovery based on IP address.
    - **ARP Request**: Broadcast packet requesting MAC address from the device that owns the destination IP address. If there is no response, ARP signals a mistake.
    - **ARP Reply**: Owner of the destination IP address sends back it's MAC address using unicast packet. MAC address is recognised from body of ARP packet, not Ethernet header.
    - **ARP Table**: Table that temporarly holds discovered MAC addresses. Contains pairs of IP and MAC addresses. Every row has aging time.
- **ICMP - Internet Control Message Protocol**: For sending control messages about work of IP network.
    - **Encapsulated in IP message**: Techincally is appearing as protocol of transport layer, but does not do transport layer functions.
    - **Two base groups**: *Error Message* and *Query Message* (request and reply).
    - **ICMP - Destination Unreachable**: ICMP Error Message.
        - **Error message**: Informing source device that the packet was thrown away. Contains first 100 bytes of the original packet, so device could recognise which packet was thrown away.
        - **Types**: 
            - **Can't Fragment**: When IP packet is larger than MTU value in next L2 segment, and "Don't fragment" flag is set.
            - **Network Unreachable**: When there is no matching network in routing table.
            - **Host Unreachable**: When there is no response for ARP Request in the directly connected network.
            - **Protocol Unreachable**: Packet got to the L3 of the destination device, but L4 protocol is unknown to the device.
            - **Port Unreachable**: Packet got to the L4 of the destination device, but there is no application ("open port") that is given in the L4 header.
    - **ICMP - Redirect**: ICMP message.
        - **Error message**: Default gateway informs the sender device that for the destination there is a better specific route (more routers connected to same LAN).
        - **Steps**:
            1) Device sends packet for other network to default gateway.
            2) Default gateway forwards the packet to another router on the same LAN (receives and sends to the same interface - sign of error).
            3) Default gateway informs the device that there is a better route.
            4) New specific route is being written in routing table of the device.
            5) Device sends new packets directly to the other router using newly written route.
    - **ICMP - Time Exceeded**: ICMP Error message.
        -  **Error message**: When Time-To-Live reaches zero, packet is being thrown away, of which the router is informing the source device.
    - **ICMP - Echo Request/Reply (ping)**: ICMP Query message.
        - **Ping command**: Checks reachability on IP layer.
        - **Steps**:
            1) Sends ICMP Echo Request to chosen IP address.
            2) Gets reply with ICMP Echo Reply message.

## Routing Protocols

- **Routing protocols**: Not for routing concrete messages, but for routers to learn how to route messages - to set up routing tables.
- **Base principles**:
    - **Routing update**: Inform other routers about networks for which they have information.
    - **Gather information**: Gather information about other networks from other routers.
    - **Best route**: If there are more routes to some network, best one is chosen based on certain metrics and that route is written in routing table.
    - **Topology change**: If topology change happens, best route is again being chosen based on metrics and other routers are informed about new state.
- **Autonomous System**: Unique computer networks administrative domain.
    - **NOC**: *Network Operation Center* - center with unique control of whole network.
    - **Address space**: Careful design and management of unique address space.
    - **Synced routing**: Configurations of routers and adjustments are synchornized in whole network.
    - **Requirement**: In order for a network to be an autonomous system it must be connected to at least two autonomous systems (~100.000 systems today).
    - **Internal routing protocols**: Inside one autonomous system.
        - **Routing domain**: Part of network with one routing protocol. Autonomous system usually has one routing domain, but can have more.
    - **External routing protocols**: Between autonomous systems, more precisely between "border routers".
        - **Internet**: BGP external routing protocol between autonomous systems.
- **Distance Vector**: Internal routing protocol.
    - **Communication exchange**: Adjacent routers exchange information about networks, based on which they find out:
        - **Metric**: Distance to certain network.
        - **Vector**: Vector that leads to certain vector - next-hop.
    - **Vision**: Routers know only adjacent routers, not whole topology. Routes are periodically exchanged.
- **Link State**: Internal routing protocol.
    - **Communication exchange**: Adjacent routers exchange information about networks, whole topology is found out, with all parameters (link bandwidth, addresses, ...).
    - **Topology change**: Informations aren't exchanged periodically, only upon topology change.
- **Classful routing protocols**:
    - **Masks**: Routes that are being exchanged do not contain masks. Masks are supported but have to be same length in all IP networks (all routers know the mask implicitly based on their interface configuration).
    - **Autosummarization**: Automatic aggregation of all IP networks when communicating with other routing protocol. It is classful - done one network part of class A, B, or C independently of the mask that is being used.
- **Classless routing protocols**:
    - **Masks**: Masks are contained in routes that are being exchanged between routers.
    - **VLSM**: Mask of variable length.
    - **Aggregation**: Flexible aggregation of IP networks - transmitting aggregated routes to other routing domain.
    - **Modern use**: Only they are being used for a long time.
- **Metric**: For choosing best route when there are more different routes to some network. Can be:
    - **Hop count**: Number of steps (routers) to certain network.
    - **Bandwidth**: Calculated from link speed.
    - **Cost**: Arbitrary predefined price.
    - **Delay**: Delay that link has (for example satellite links have higher delay than ground links, independently from bandwidth).
    - **Load**
    - **Reliability**
- **Load Balancing**: More routes to certain network with same metric.
    - **Communication stream**: Usually one communication stream (all packets from same communication) goes one link, other stream on other link.
    - **Routing table**: Routing table can contain two or more next-hop addresses for one network.
- **Administrative distance**: Used when two different routes to the same network are received from different routing protocols.
    - **Fixed price**: Every routing protocol has predefined fixed price (RIP - 120, OSPF - 110, ...).
    - **Choosing**: Router chooses the route from the protocol with smaller administrative distance (price).

## Distance Vector

- **Routing update**: Information exchange with adjacent routers - address of network (with mask) and metric to that network.
- **Perodic announcement**: Routers periocially send routes from their routing table, even when there are no changes.
- **Convergency**: Process of setting up stable and consistent state on all routers in network.
    - **Stable state**: Routing tables aren't being changed on new routing updates.
    - **Consistent state**: All routes are valid, no irregularities.
- **Routing loops**: Can occur during convergence and create unconsistent state of routing tables and loops upon routing.
    - **"Count-to-Infinity" Problem**: One network is shut down, deleted from table A, table B still hasn't deleted that network and sends routing update. Table A gets routing update from B and adds previosly deleted network with +1 hop count. Table A sends routing update, and table B receives new information about network and updates it to +1 hop count. And like that to infinity.
    - **Set infinity**: Set fixed maximum value for "infinity" for which when hop count gets to, declare both routes invalid and delete from both routers.
    - **Route Poisoning**: Announcing that the route is unreachable by deleting it from the table and announcing it with "infinity" metrics. Routers that receive route with "infinity" metrics write down this route (route is invalid) and keep it certain time.
    - **Triggered Update**: When route becomes unreachable, in the same momemnt announcment is made, not waiting for the next periodic routing update. Only one route is announced, not whole routing table. Much faster convergence.
    - **Split Horizon**: Never announce a route on the interface from which that route arrived from.
    - **Poison Reverse**: Invalid route is being announced on interfaces from where it came from - Split Horizon rule is being suspended for this case. Router confirms that it doesen't have a better route.
    - **Holddown timer**: 
        - **Problem**: Route Poisoning, Triggered update, and Split horizon aren't enough to prevent loops in case of redundant networks.
        - **Example**: Router 1 sends Route Poisoning and Triggered update for invalid network. Router 3, before receiving them, sends routing update with valid route to the network. Router 2, in case when it is closer to Router 1, receives first Route Poisoning and then shortly after routing update from Router 3 with valid route to the network which overrides the Route Poisoning which brings the network in inconsistent state.
        - **Solution**: Wait a certain time so that information can propagate to all routers.
        - **Holddown timer**: When router receives Route Poisoning Triggered update, start Holddown timer (usually 3min). During Holddown time all new routes for that network are being ignored.
        - **Convergency**: Leads to long convergency time which is way it isn't used nowdays.
- **RIPv1**: *Routing Information Protocol*
    - **Administrative distance**: 120.
    - **Classful**: Doesn't support VLSM, automatic autosummarization.
    - **Metric**: hop-count, max - 16.
    - **Applicative layer**: RIP works on applicative layer, messages are being transmitted inside UDP messages on L4.
    - **Communication in two steps**: Every 30 seconds.
        - **RIP Request message**: Stating network address for which the routes are being requested - usually 0.0.0.0 for all routes. Sent on broadcast address.
        - **RIP Response message**: Response on request - usually all routes (whole routing table). Up to 25 routes in one message. Sent on unicast address to the router that sent request.
- **RIPv2**:
    - **Classless**: Support for VLSM. Mask is being transmitted in routing updates.
    - **Mutual authentication**: For security.

## Link-State

- **Link-State Advertisements (LSA)**: Adjacent routers exchange much larger set of information.
- **Link-State Database (LSDB)**: Base of information is created using which the topology of network is reconstructed (router graph and network with metric). Contains all LSA received from all routers, in the end all routers will have the same database.
- **Shortest Path First (SPF)**: Shortest distance to every network is being calculated using Dijkstra's algorithm by which the routing table is being created, if more routes have same price then load balancing is done by writting all of them in the table.
- **"Link"**: Routers interface - describes the network.
    - **"Link state"**: Information about interface. IP address and mask of network, IP address of interface, router ID, interface type, link cost, adjacent routers on the link, ...
- **LSA packet**: Contains: State of every directly connected link (interface); Information about neighbours - router, link type, cost (bandwidth).
- **Flooding**: Intensive exchange of LSA packets by sending them to every directely connected router, and those routers forwarding them to their direct neighbours.
- **Area**: Grouping routers and IP networks in distinct areas. Link failures are localized, and flooding is done only in that area. Doesn't invoke convergency in other areas. Larger scalability.
- **Fast convergency**: Flooding is done initially upon turing on routers and upon every topology change. More memory, CPU time required, and bandwidth required upon convergency. The load is minimal during stable state - only *keepalive* messages are sent.
- **Two kinds of Link-State**:
    - **OSPF**: *Open Shortest Path First*, Administrative distance - 110, Classless.
    - **IS-IS**: *Intermediate System-Intermediate System*, ISO standard, Administrative distance - 115.

## OSPF
- **OSPF messages**: Hello, DD, LSR, LSU, LSAck - encapsulated in IP packets (do not belong to transport layer).
- **Hello process**: Protocol for establishing neighbor routers. 
    - **Hello message**: Requirment for neighbors to be established is that they have same parameters:
        - **Network IP address**: They must be connected to the same IP network.
        - **Hello interval**: Period of announcing Hello messages (10sec on Ethernet connections).
        - **Dead interval**: Time for terminating neighbor - when no Hello messages arrive (4x Hello interval).
        - **Area ID**: They must belong to the same area.
        - **Authentication**: Optional.
        - **Other parameters**: "Stub area flag", ...
    - **Loopback interface**: Logical interface (not physical, exists only in software). Contains arbitrary IP address and mask (mask can even be "/32"). Always active. Good for accessing router (ping, logging, ...).
    - **Router ID (RID)**: Unique router identifier on OSPF protocol layer. It is equal to: Largest IP address of physicall interface if loopback isn't defined. Largest IP address of loopback interface, if it exists.
    - **Process**:
        1) **Down**: Initial state.
        2) **Init**: After turning on the interface, ready for sending Hello messages.
        3) **2-way**: Neighbors set up, with next conditions: RID is recognised in "seen" field that contains all discovered neighbor routers on that segment and is equal on both routers.
- **ExStart process**: Exchange preparation.
    - **Slave / Master**: Negotiating who is master and who is slave. Master - higher RID.
    - **Sequence Number (Seq)**: Numeration of route information. Incremented when new information appears.
    - **Process**:
        1) Router A suggests that he is Master and sets up Seq.
        2) Router B has higher RID, and becomes the Master and sets up Seq, and sends it to router A.
        3) Router A accpets Seq and becomes Slave.
- **Exchange process**: Descriptor exchange - LSA data from LSDB tabels. Goal is to determine what information is missing in routers LSDB.
    - **Database Description (DD)**: Packets containing only data descriptions, not whole information.
    - **Process**:
        1) Master starts communication, by sending DD packets.
        2) Seq is incremented - it identifies sent packets for tracking if some packet got lost, if lost then retransmission.
- **Loading process**: Exchanging missing information.
    - **Link State Request (LSR)**: Master states descriptor list of missing informations.
    - **Link State Update (LSU)**: Slave answers with one or more packets that contain all missing information.
    - **Link State Acknowledgement (LSAck)**: Information received confirmation.
- **Full**: Finished state - LSDB tables syncronized.
- **Multiple routers in one Ethernet network**:
    - **Designated Router (DR)**: To avoid too much neighbor connections (O(n^2)), we define one central router upon establishing neighbors.
    - **Backup Designated Router (BDR)**: Reserve central router.
    - **DROthers**: Rest of the routers.
    - **SLA exchange**: Exchange of SLA packets is done through DR. DROhers send LSA packet on multicast address (AllDRouters - 224.0.0.6). DR and BDR "listen" the traffic for AllDRouters multicast address and receive LSA. Only DR (not BDR) forwards LSA packet on multicast address (AllSPFRouters - 224.0.0.5). All OSPF routers "listen" the traffic for AllSPFRouters multicast address and receive LSA.
    - **Priority**: Priority upon choosing DR and BDR. Every router interface has its assigned priority (value from 0 to 255). Value 0 means that this router doesn't participate in election of DR and BDR. Contained in Hello messages. Higher value is higher priority.
    - **Election**: Router with highest priority becomes DR, with second highest becomes BDR, if priorities are same, the one with higher RID is choosen.
    - **Removing/Adding routers**: When new router is added, DR and BDR aren't changed even if the new router has higher priority. When DR is removed, BDR becomes DR, and BDR is some other router with highest priority (can happen that new BDR has higher priority than DR).
- **OSPF metric**:
    - **Cost**: Equals to cost = 10^8 / bandwidth. Smaller price - higher priority.
    - **Serial interface cost**: Serial interfaces have predefined cost no matter the bandwidth speed (cost = 10^8 / 1544kbps, (T1 line)).
    - **Custom cost**: You can define your own custom cost for every interface.
- **OSPF Areas**:
    - **Central area**: Area 0 (Backbone Area, Transit Area).
    - **Peripheral area**: Area n (n - integer value). All peripheral areas must be exclusively connected to the central area.
- **OSPF Routers**:
    - **Area Border Router (ABR)**: Border router between two areas (central and peripheral).
    - **Autonomous System Boundry Router (ASBR)**: Border router between OSPF domain and some other routing domain.
    - **Internal Router**: Internal router that belongs only to one area.
    - **Backbone Router**: Internal router that belongs to the central area.
- **Types of LSA**:
    - **Router LSA**: Type 1 (in routing tables labeled with "O" - intra-area). Generated by all routers, give informations about all interfaces. Propagated only inside one area, aren't transmitted between areas.
    - **Network LSA**: Type 2 (in routing tables labeled with "O" - intra-area). Generated by DR router. Ethernet network is announcing itself to other routers in the area. Propagated only inside one area, aren't transmitted between areas.
    - **Summary LSA**: Type 3 and 4 (in routing tables labeled with "O IA" - inter-area). Generated by ABR using Router LSA and Network LSA. It is transfered in all areas. Reduces flooding. Changes in one area don't lead to recalculating SPF in other areas. Goal is to aggregate all IP networks from one area - offloads other areas.
    - **External LSA**: Type 5 (in routing tables labeled with "O E1" and "O E2"). Generated by ASBR. Contains information about networks from outside of OSPF domain.
- **Types of areas**: Divided by the type of LSA packets that enter them.
    - **Standard Area (Ordinary)**: Contains Router LSA and Network LSA. Can accept all types of LSA, even Summary and External LSA. Backbone Area is always Standard Area.
    - **Stub Area**: Peripheral area, doesen't accept External LSA. Contains only local LSA inside this area - intra-area LSA. ABR routers automatically generate default route and insert it in this area (for traffic outside this OSPF domain). "Stub flag" - must be set on all routers to Stub Area.
    - **Totally Stubby Area**: Peripheral area, doesen't accept External LSA nor Summary LSA. Contains only local LSA inside this area - intra-area LSA. ABR routers automatically generate default route and insert it in this area (for traffic outside this area). "Stub flag" - must be set on all routers to Totally Stubby Area. Must have only one link to Backbone Area (one ABR router).
- **Virtual links**: Possibility to connect physically one peripheral area to another one (instead of backbone), but create logical link (tunnel) to ABR of Backbone Area through that middle peripheral area.
- **Route redistribution**: Route exchange between different routing protocols. Router that is in between two routing protocols must be configured to do redistribution. Internal routers in OSPF label routes to devices in other routing protocol as external and add them to their routing table. Internal routers in RIP just add routes to their routing tables.

# Transport layer

## General

- **Layer communication**:
    - **Horizontally**: End-to-end communication between two devices.
    - **Vertically**: Link between application and network layer.
- **Goal**: Maintaining communication between applications on both sides.
- **Transport of application data**: Encapsulation and decapsulation - adding and removing L4 header.
- **Two types of transmission**:
    - **Byte-stream**: Segmentation of byte stream to arbitrary size (TCP).
    - **Message-stream**: Transmission and encapsulation of whole messages (UDP).
- **Multiplexing and Demultiplexing**: For application data.
    - **On sender side**: Labeling application upon receiving data from application.
    - **On receiver side**: Recognising labeled application and forwarding data to it.
- **Port**: It is a field in L4 header that identifies application (or her part). Same as field "Type" for L2 that identifies protocols of L3, and field "Protocol" for L3. that identifies protocols of L4.
    - **IANA**: Gives fixed ports for specific applications.
    - **Port types**:
        - **Well-known Ports**: 0-1023 - only for server applications. TCP: 22 - SSH, 23 - Telnet, 80 - HTTP, 443 - HTTPS; UDP: 53 - DNS, ...
        - **Registered Ports**: 1024-49151 - for client and server applications.
        - **Private (Dynamic) Ports**: 49152-65535 - only for client applications.
- **Socket**: Unambiguous identification of application on network (or part of application that achieves communication). "Entry" identification in application upon communication. Contains: IP address, Transport protocol id (TCP or UDP), Port number.
- **Type of application**:
    - **Server application**: Available for access from any users. They have socket with known IP address and TCP or UDP port.
    - **Client application**: Application on users end that initiate communication with server application. They have socket with arbitrary IP address and dynamically allocated TCP or UDP port.
    - **Two-way communication**: Communication between client and server sockets. Request from client to server. Response from server to client.
- **Additional functions**:
    - **Connection oriented**: Establishing and maintaining communication session.
    - **Reliable delivery**: Guaranteed reliable delivery of all application data as a whole. Lost or damaged segments are detected and sent again.
    - **Ordered data reconstruction**: Through different routes, segments can arrive in changed order, but receiving end reconstructs them in original order.
    - **Flow control**: Dynamic increasing and reducing of data stream. Controlling data transfer based on capabilites and current load of the network.
- **Transport protocols**:
    - **UDP**: *User Datagram Protocol*.
        - **Basic functions**: Has only basic functions.
        - **Connectionless**: Simple, no guarantee of reliable transfer and order. Small amount of processing - low device load.
    - **TCP**: *Transmission Control Protocol*.
        - **Additional functions**:  Has basic and additional functions.
        - **Connection oriented**: Larger amount of processing - bigger device load.
- **UDP**:
    - **Datagram**: Messages, received from application, that are being transmitted as a whole.
    - **UDP header format**:
        - **Source port, Destination port**: Both have 2B.
        - **Length**: Length of data including header. Maximum data length: 65535-8-20 = 65507B. Reduced by 8B of UDP header and 20B of IP header.
        - **Checksum**: Error checking - 2B. First complement of UDP header, data, and pseudo-header (source and destination IP address, UDP protocol identification, and UDP packet length).

## TCP

- **Point-to-Point**: Unicast communication between two devices. TCP doesn't support broadcast or multicast.
- **Full-Duplex**: Independent communication of two directions. Even when applicative data is transmitted only in one direction, control data are transmitted in other direction.
- **Segmentation**: On senders end. Dividing larger units in to, so called, segments. MSS - Maximum Segment Size (default value 536B, defined upon establishing connection).
- **Reassembling**: On receivers end. Reconstruction of original application data byte stream.
- **TCP header format**:
    - **Source, Destination port, Checksum**: Like in UDP.
    - **HLEN**: *Header Length** - 4 bits. Length in units of 4B.
    - **Window Size**: Total number of bytes that can be sent before expecting confirmation.
    - **Options**: Different options, variable length.
    - **Sequence Number (SEQ)**: Initally random value determined upon establishing connection. Every single byte in stream of application data has its own ordinal number relative to initial SEQ. It achieives identification of segments and maintaining segment order upon receiving.
    - **Acknowledgement Number (ACK)**: Confirmation of receiving contiunal stream of bytes. Represents relative ordinal number (SEQ) of the next byte that is expected for receiving. Achieves reliable transmission of segments.
    - **Flags**: Control flags that describe packet meaning and meaning of other fields in the header.
        - **SYN**: *Synchronization* - Initialization of Sequence Number value.
        - **ACK**: *Acknowledgment* - Acknowledgement Number field is valid.
        - **FIN**: *Finish* - Last segment, finished connection in one direction.
        - **RST**: *Reset*.
- **Establishing TCP session**: Two-way communication (full-duplex). Two separate communication sessions and two separate pairs of Sequnce and Ackowledgement Number. 
    - **Request**: Setting up random SEQ value, and turning on SYN flag.
    - **Response**: Confirmation of receiving (ACK = SEQ + 1), turning on ACK flag (no data, 0 bytes). Denying request, turning on RST fleg (for example: no application with given port).
    - **Three-way handshake**:
        1. **Active Open state**: Requesting - or so called "syncronization".
        2. **Established state**: Confirming session in first direction with response and request for opening session in other direction, also in that response message.
        3. **Established state in both directions**: Confirming session in other direction.
    - **TCP socket**: Entry in to the application only for paired side. Can be viewed as 5-tuple: srcIP, srcPort, dstIP, dstPort, TCP.
- **Breaking TCP session**:
    - **Two-way handshake**:
        1. When one side doesen't have any more data for sending, FIN flag is sent.
        2. Other side acknowledges receiving last packet by sending ACK for that packet. Session is closed.
    - **2x Two-way handshake**: Steps 3. and 4. are for closing session in other direction.
    - **Three-way handshake**:
        1. Send FIN flag
        2. Confirm receiving FIN flag by sending ACK, send FIN in same packet as ACK if other side doesen't have any more packets to send.
        3. Confirm receiving last packet by sending ACK.
- **Timeout**: Determined time that is being waited before retransmitting segment again. This timer should be greater than RTT (Round Trip Time).
    - **RTT estimation**: RTT = a*RTTold + (1-a)*RTTnew. RTTnew - last sent and confirmed segment. RTTold - previous estimation. a - factor from 0 to 1 (bigger value - larger impact from RTTold, slower changes).
    - **Timeout calculation**: Timeout = b * RTT. b - scaling factor (usually b = 2).
- **Error Recovery**: Based on SEQ value it knows the place of data. ACK is sent only when some segment arrives. ACK value represent last segment (byte) in continuity. Same ACK multiple times means one segment is lost, but others are successfully received.
- **Segments reordering**: Different segments can arrive through different routes which can lead to mixed order of receiving segments. Receiving end will reconstruct original order based on SEQ value of received segments.
- **Flow control**: Window mechanism - done on the sender end. Done independently in both direction. Window contains part of application data that are being sent. Flow control is achieved by establishing window size.
    - **Before window**: Sent data (segments) for which ACK is received.
    - **In window**: Sent data (segments) for which ACK is waited and data that is ready to be sent. 
    - **After window**: Data that can't be sent.
    - **Sliding Window**: Window is being moved when it gets ACK for the segment in the windows begining.
    - **Dynamic Window**: Initially both ends make an agreement on windows size when they establish connection. In case of too much load in receiving end or packet loss, sender can be requested to reduce the window size (slows down sending of new segments). If there are no error, window size can be gradually increased.
- **Congestion Control**: Sender is dynamically adjusting to current load.
    - **Slow Start**:
        - **Advertised Window (AW)**: Inital window size value defined upon establishing connection - set by receiver to control speed of receiving segments.
        - **Congestion Window (CW)**: To avoid congestion, sender gradually increases real window size (sending speed) until reaching maximum value (AW).
        - **Initial CW value**: Initial value for CW is usually 1 segment, it gets increased with every ACK. 
        - **Increasing CW value**: If every segment is acknoweldged, CW is multiplied by 2 in every step (grows exponentially). Typically one ACK is sent for 2 segments, but growth is still exponential. 
        - **Timeout**: If timeout occurs - segment loss, new Slow Start.
    - **Congestion Avoidance**: Linearly increasing window, instead of exponentionally.
        - **ssthresh**: *Slow Start Threshold Size*, Window size until which exponential growth occurs in slow start phase. CW > ssthres - Congestion Avoidance (linear). CW < ssthresh - Slow Start (exponential). If ACK doesen't arrive for some segment, ssthresh is reduced to half of CW's last value (ssthresh = CW/2).
    - **Fast Retransmit**: Retransmitting segments before timeout timer. Happens when multiple ACKs with same value arrive meaning that certain segment is lost (or it came to order change). 1 or 2 same ACK - segment maybe isn't lost, maybe it came to order change. 3 same ACKs - segment is actually lost, retransmit it.
    - **Fast Recovery**: Happens after Fast Retransmit. Window size is reduced to sshtresh instead of Slow Start again, going directly to Congestion Avoidance.

# Application layer

## Protocols

- **WWW**: *World Wide Web* - web service.
- **HTTP**: *HyperText Transfer Protocol* - for transmitting textual messages with special tags and nested structure (HTML - HyperText Markup Language). Binary data are referenced and transmitted as separate objects (pictures, audio, video). TCP port - 80.
- **HTTPS**: *Secure HTTP*. TCP port - 443.
- **Maintaining connection**:
    - **Non-Persistent mode**: TCP connection is established upon every query and after that broken.
    - **Persistent mode**: TCP connection is established and used for multiple queries for some time, even if it isn't used (timeout).
- **Connection tracking**:
    - **Stateless**: Client activity isn't remembered.
    - **Stateful**: Client activity is remembered by web sites (cookie).
- **Proxy**: Intermediate server for HTTP protocol. Previosly requested pages are cached and saved for some time. For repeated request, even from another user, cached data is returned. Advantages: Faster response, Increased user privacy, Filtering traffic, Enabling access to certain content that is accessible only trough proxy server.
- **FTP**: *File Transfer Protocol*.
- **Email service**:
    - **SMTP**: *Simple Mail Transfer Protocol* - for sending emails.
    - **POP3**: *Post Office Protocol, v3* - for receiving emails.
    - **IMAP**: *Internet Mail Access Protocol* - for receiving emails.
- **Remote access**:
    - **Telnet**: Remote access to CLI. Not used today because it isn't encrypted.
    - **SSH**: *Secure Shell* - encrypted remote access to CLI.
    - **RDP**: *Remote Desktop Protocol* (Microsoft) - remote access to graphics console. RDP client - Remote Desktop Connection.

## DNS

- **Domain Name System (DNS)**: Service for translating names in to IP addresses. Maps symbolic names in to IP addresses. It has distributed defining and translation. "hosts.txt" file exists locally in operating systems and enables name translation without DNS.
- **DNS structure**: Name hierarchy in tree topology. Tree root - root domain labeled with empty string (""). Tree node - symbolic name.
    - **FQDN**: *Fully Qualified Domain Name* - Name of the nodes divided by dot character in route to the root.
    - **Relative domain name**: Subdomain of some domain, implicitly implied full name of domain or subdomain based on the context.
    - **Name**: Every label can have maximum of 63 characters. Maximum length of full name is 255 characters. ASCII characters, Case-insensitive.
    - **TLD**: *Top Level Domains* - subdomains of root domain. For example: com, edu, gov, net, org, mil. Global root domain "" - belongs to SAD.
    - **ccTLD**: *County Code TLD* - belong to individual countries. For example: yu - Yugoslavia, rs - Republika Srbija, sr - Surinam, eu - European Union.
- **DNS organization**: Logical structure is physically organised in distributed way - whole tree is divided in zones.
    - **Zone**: Part of the tree (one or more nodes). Contains information about nodes that belong to it (usually only one node - domain). Administratively belongs to one unit (firm, university, country, ...). Textual file is defined on one server - DNS server or NS (Name Server).
    - **Zone Delegation**: Domain zone defines names of subdomains, while rest of subdomains data is defined in separate zones. Domain topology is technically fully independent of topology of physical connections in network (Devices from one domain can belong to different, physically separate and remote networks).
    - **Primary DNS server**: DNS server on which zone is defined for some domain. All data for that domain and definitions of subdomains.
    - **Secondary DNS server**: DNS server that periodically takes zone from primary DNS server - transfer of the zone. It is recommended that there is at least one secundary DNS server for every domain.
    - **Authoritative DNS servers**: DNS servers that have whole zones for certain domains.
- **DNS Resolver**: Part of DNS software that resolves names (pair names with IP addresses).
    - **On clients end**: If there is no data about name in local cache - send query to locally set up DNS server.
    - **On servers end**: If there is no data about name in local cache or zone base - send query to other DNS servers, authoritative for belonging domain.
    - **Recursive query**: DNS server returns complete answer as a whole or error. Generally meant for client queries to a server.
    - **Iterative query**: DNS server return  incomplete "best possible" answer - refers to other servers in the hierarchy that can resolve the query. Usually done from one DNS server to other DNS servers.

# Additional protocols

## DHCP, NAT, ACL

- **Static assignment of IP addresses**: Manually assigning fixed IP addresses by configuring every device.
- **Dynamic assignment of IP addresses**: Automatic assigning of IP addresses, masks, and defualt gateways. Configuration on one place - server.
    - **RARP**: *Reverse Address Resolution Protocol*.
    - **BOOTP**: *BOOTstrap Protocol*.
    - **DHCP**: *Dynamic Host Configuration Protocol*.
- **RARP**: Reverse ARP. ARP - find MAC address based on IP address. RARP - find IP address based on MAC address.
    - **RARP server**: Manually maps MAC address in to certain IP addresses.
    - **RARP Request**: Device upon turing on generates RARP Request packet and sends it to MAC broadcast address. All devices receive it, only RARP server recognises and finds its IP address in its MAC address table.
    - **RARP Reply**: RARP server generates response. Device that initiated request accepts the packet, takes the IP address, and start using it.
- **BOOTP**: Assigning IP address based on MAC addresses (similarly to RARP).
    - **BOOTP server**: Manually maps MAC addresses in to certain IP addresses. Additionally it can send Default Gateway, Mask, and DNS server.
    - **BOOT-REQUEST message**: Device upon turning on generates this request. Contatins MAC address of the sender, broadcast IP and MAC address in destination field. Only BOOTP server accpets it.
    - **BOOT-REPLY message**: Send back information.
- **DHCP**: Upgraded version of BOOTP. Dynamical assigning of IP addresses from predefined range.
    - **DHCP-DISCOVER message**: Equivalent to BOOT-REQUEST message.
    - **DHCP-OFFER message**: DHCP server assigns free IP address from range of reserved IP addresses. Generates and sends offer. DHCP server can check if some IP address is taken using ICMP ping packet.
    - **DHCP-REQUEST message**: Device accepts address from first DHCP-OFFER message and sends request to use this address.
    - **DHCP-ACK message**: All DHCP servers accept DHCP-REQUEST message, only the one that offered the IP address generates this message.
- **NAT**: *Network Address Translation*. Most used case - translation of private address in to public ones. Done on border router.
    - **Inside Local Address**: Address assigned to host in internal network which addresses are being translated.
    - **Inside Global Address**: Legitimate (Internet) IP address assigned from provider. Address in which Inside Local address is being translated to.
    - **Outside Global Address**: Devices IP address on external network.
    - **Static NAT**: Physical one-to-one mapping. Not used.
    - **Dynamic NAT**: NAT table is dynamically filled with pairs of local and global address.
        - **Pool**: Defined set of global IP addresses that is being used.
    - **Overload NAT**: Multiple local addresses simultaneously use one global address.
        - **PAT**: *Port Address Translation* - used to solve ambiguity when multiple local address use one global address, by translating local IP address using port number and assigning it a new global addresses with possibly new port number. NAT table can change port value in global address.
        - **Port forwarding**: Static mapping for certaing addresses and ports for setting up servers in internal networks. Flaw: only one local IP address can be paired with server port.
- **ACL**: *Access Control Lists*, Allowing and forbidding packet traffic through router interface. Inspection on L3 and L4.
    - **Condition**: Comparing IP addresses, TCP/UDP ports, ICMP messages.
    - **Action**:
        - **Permit**: Forward packet.
        - **Deny**: Destroy packet.
    - **Packet Filtering**
    - **Direction**:
        - **In**: Packets that enter router interface.
        - **Out**: Packets that exit router interface.

## IPv6

- **Need of IPv6**: Exponential growth of Internet and connected devices, lack of IPv4 address space.
- **Characterstics**: 
    - **Large address space**: Much larger address space than IPv4.
    - **Efficient routing**: Smaller number of external routes on Internet. Hierarchical structure of network addresses allows more efficient aggregation. Simpler headers for more efficient packet processing.
    - **Automatic configuration**: Supports automatic device configuration.
    - **Security**: Supports data security with IPSec implementation.
    - **Mobile devices**: Better support for mobile devices.
    - **QoS**: Built in support for resource allocation and quality of service (QoS).
    - **Multicast addresses**: Larger number of multicast addresses.
- **Header**:
    - **Removed fields**: Fields that were used in IPv4, but removed from IPv6.
        - **Header Length**: IPv6 header has fixed length, options are moved in to separate headers.
        - **Header Checksum**: Packet integrity check is already done on L2 layer. TCP/UDP contains Checksum field that uses IP address from this header (pseudo-header).
        - **Fragmentation fields**: "Identification", "Flags" and "Fragment Offset" are removed because fragmentation is expensive process that allocates resources on receivers end, introduces new timers and waiting in case of fragment loss, and fragment loss results in whole packet loss.
            - **Solution**:  Fragmentation is done in source device, not in routers.
            - **MTU**: IPv6 guarantees MTU of at least 1260B.
            - **"Packet Too Big"**: In case that router cannot forward packet because it is larger than MTU on the link, it destroyes it and generates ICMPv6 message "Packet Too Big".
            - **Path MTU Discovery**: Finds smallest MTU value on whole path to destination. Sends packet of certain size and checks if it gets "Packet Too Big".
            - **Problem**: Routing is dynamic and route can change during communication, but this happens very rarely.
    - **IPv6 fields**:
        - **Payload Length** (16 bits): Length of data in bytes.
        - **Traffic Class** (8 bits): Same as "ToS" (Type of Service) field in IPv4. Source generates packets that belong to different traffic classes with different priorities.
        - **Flow Label** (20 bits): Flow represents communication between application source and destination. Flow Label uniquely labels each flow. Only first packet is being routed and Flow Label paired with exit port is being cached. Much faster routing - new packets of same flow do not require routing.
        - **Hop Limit** (8 bits): Same as "TTL" (Time To Live) field in IPv4.
        - **Next Header** (8 bits): Instead of "Protocol" field in IPv4. Identifies next header which can be: header of higher layer (TCP, UDP, ICMPv6, OSPFv3, ..), or header with IPv6 options. Option headers also contain "Next Header" field so multiple options can be chained before moving on to higher layer.

<table border="1" cellspacing="0" cellpadding="4">
  <tr>
    <th align="center" colspan="8">1. byte</th>
    <th align="center" colspan="8">2. byte</th>
    <th align="center" colspan="8">3. byte</th>
    <th align="center" colspan="8">4. byte</th>
  </tr>
  <tr>
    <td align="center" colspan="4">VERS</td>
    <td align="center" colspan="8">Traffic Class</td>
    <td align="center" colspan="20">Flow Label</td>
  </tr>
  <tr>
    <td align="center" colspan="16">Payload Length</td>
    <td align="center" colspan="8">Next Header</td>
    <td align="center" colspan="8">Hop Limit</td>
  </tr>
  <tr>
    <td align="center" colspan="32">Source IP Address</td>
  </tr>
  <tr>
    <td align="center" colspan="32">Destination IP Address</td>
  </tr>
  <tr>
    <td align="center" colspan="32">Data</td>
  </tr>
</table>

- **Source routing option**: Option header defines number of segments and sequnce of intermediate points, where the last address is destination address. Destination address of regular IPv6 header is address of first intermediate point. When router recognises himself as destination and there is a source routing header it decrements number of segments and sets next defined router as destination.
- **IPv6 Addresses**:
    - **Length**: IPv6 address has length of 16B (128 bits). 
    - **Hexadecimal**: It is written in hexadecimal (one hexadecimal digit of 4 bits is called "*nibble*").
    - **Mask**: Mask is used in prefix notation ("/n").
    - **Format**: Eight groups of 4 hexadecimal digits separated by ':' (1111:aaaa:2222::bbbb:3333:cccc:4444:dddd/mask).
    - **Shortened notation**: 
        1. Throw out leading zeros in groups of 4 digits (":000x" -> ":x"). 
        2. Throw out only one subarray of groups consisted of zeros (":0:0:0:" -> "::").
- **Types of IPv6**:
    - **Unicast**: Unique address, identifies interface.
        - **Global Unicast**: Public addresses available on Internet. Range - 2000::/3 (start with binary value "001").
            - **Prefix**: Network part of the address.
                - **Global Routing Prefix**: Typically first 48 bits - assigned to providers and other users.
                - **Subnet ID**: Typically 16 bits - subnets inside of base network.
            - **Interface ID**: Typically  last 64 bits - interface address in IPv6 network (equivalent of IPv4 host part). Network part, or the mask, can "enter" in Interface ID but it is a bad practise and usually there is no need for that.
                - **EUI-64**: *Extended Unique Identifier*, Rule of generating Interface ID based on MAC address.
                - **Random**: Can be assigned with pseudo-random array of bits (default for Windows PCs).
        - **Unique Local**: Private addresses - meant for use in private networks. Range - fc00::/7. Can't be seen on Internet.
        - **Link Local**: For use only in local IP network (L2 segment). Range - fe80::/10. Routers don't forward these packets. Most devices have two IPv6 addres - one Global Unicast or Unique Local, and one Link Local address. They have special use. Its Interface ID part is defined by EUI-64.
        - **Loopback Address**: ":1/128".
        - **Unspecified Address**: "::/128". Can be used as source address.
        - **Embedded IPv4 Address**: Used for transition from IPv4 to IPv6.
    - **Multicast**: Address that identifes multiple interfaces of different devices based on common purpose. Range - ff00::/8.
    - **Anycast**: Used when multiple different devices have same IPv6 address. Packets get to one closest device (defined by metric and routing protocol). Devices (usually servers, for example DNS servers) configure Anycast address to be accessed by the closest device to improve delivery time.
- **IPv6 address configuration**: Can be static (unpractical) or dynamic.
    - **Stateful DHCPv6**: Like DHCP for IPv4 and it remembers which device got which address.
    - **Stateless Address Autoconfiguration (SLAAC)**: Devices find out network part of 64 bits, default gateway, and DNS server (optionally). Interface ID is automatically set by EUI-64 or random choice.
        - **ICMPv6 Neighbor Discovery Protocol (NDP)**: It replaces ARP by using ICMPv6 messages. It uses *Router Solicitation* (RS), *Router Advertisement* (RA), *Neighbor Solicitation* (NS) and *Neighbor Advertisment* (RA) messages.
        - **Process steps**:
            1. Device sends request to router using Router Solicitation message which contains:
                - **Source IP address**: Predefined Link-Local device address.
                - **Destination IP address**: Multicast address *"All IPv6 Routers"* (FF02::2).
            2. Router responds with sending Router Advertisement message which contains:
                - **Source IP address**: Link-Local router address.
                - **Destination IP address**: Link-Local device address.
                - **Default Gateway**: Source IP address is used as default gateway.
                - **Content**: Network address (prefix), and optionally DNS.
        - **Periodical RA messages**: Independently from RS message, routers on their own periodically announce RA messages using multicast address as destination (*All IPv6 Devices* - FF02::1). For example, Cisco routers use 200 seconds as announcing period.
- **Address Resolution**: Equivalent to ARP protocol - looking for MAC address based on given IPv6 address. Done in two steps:
    1. Device sends request using Neighbor Solicitation (NS) message which contatins:
        - **Source IP address**: Unicast address of device that requests MAC address.
        - **Destination IP address**: *Solicited-Node Multicast* address of device for given IP address.
        - **Destination MAC address**: Multicast - 3333.ff55.6666.
    2. Called device sends Neighbor Advertisement message which contains requested MAC address.
- **Duplicate Address Detection (DAD)**: Checks if the address we randomly generated already exists by sending request for the address using Neighbor Solicitation and waiting sometome to see if someone will answer (Neighbor Advertisiment). 