# Fundamentals of Ethernet LANs
## Ethernet Physical Layer Standards
Cabling can be UTP (with a suffix that includes T) or fiber (with a suffix that includes X)

|Speed|Name|IEEE Standart Name|Formal standart Name|Cable Type, Maximum Length|
|---|---|---|---|---|
|10 Mbps|Ethernet|10BASE-T|802.3|Copper, 100 m|
|100 Mbps|Fast Ethernet|100BASE-T|802.3u|Copper, 100 m|
|1000 Mbps|Gigabit Ethernet|1000BASE-LX|802.3z|Fiber, 5000 m|
|1000 Mbps|GigabitEthernet|1000BASE-T|802.3ab|Copper, 100 m|
|10 Gbps|10 Gig Ethernet|10GBASE-t|802.3an|Copper, 100 m|

## Building Physical Ethernet LANs with UTP
RJ-45 connector
RJ-45 Ethernet port as part of a network interface card (NIC)
enhanced small form-factor pluggable (SFP+) transceiver

* Gigabit Ethernet Interface Converter (GBIC): The original form factor for a removable transceiver for Gigabit interfaces; larger than SFPs 
* Small Form Pluggable (SFP): The replacement for GBICs, used on Gigabit interfaces, with a smaller size, taking less space on the side of the networking card or switch. 
* Small Form Pluggable Plus (SFP+): Same size as the SFP, but used on 10-Gbps interfaces. (The Plus refers to the increase in speed compared to SFPs.)

### UTP Cabling Pinouts for 10BASE-T and 100BASE-T
two pairs of wires in a UTP cable, one for each direction. Ethernet NIC transmitters use the pair connected to pins 1 and 2; the NIC receivers use a pair of wires at pin positions 3 and 6. LAN switches, knowing those facts about what Ethernet NICs do, do the opposite: Their receivers use the wire pair at pins 1 and 2, and their
transmitters use the wire pair at pins 3 and 6.
To allow a PC NIC to communicate with a switch, the UTP cable must also use a <b>straightthrough</b> cable pinout.

When two like devices connect to an Ethernet link, they both transmit on the same pins. In that case, you then need another type of cabling pinout called a <b>crossover cable</b>. The crossover cable pinout crosses the pair at the transmit pins on each device to the receive pins on the opposite device.

* Crossover cable: If the endpoints transmit on the same pin pair 
* Straight-through cable: If the endpoints transmit on different pin pairs

|Transmit on pins 1,2|Transmit on pins 3,6|
|---|---|
|PC NICs|Hubs|
|Routers|Switches|

### UTP Cabling Pinouts for 1000BASE-T
1000BASE-T requires four wire pairs. It also uses more advanced electronics that allow both ends to transmit and receive simultaneously on each wire pair. It uses the same pinouts for two pairs as do the 10BASE-T and 100BASE-T standards, and it adds a pair at pins 4 and 5 and the final pair at pins 7 and 8. The Gigabit Ethernet crossover cable crosses the same two-wire pairs as the crossover cable for the other types of Ethernet (the pairs at pins 1,2 and 3,6). It also crosses the two new
pairs as well (the pair at pins 4,5 with the pair at pins 7,8).

## Building Physical Ethernet LANs with Fiber
Components of a Fiber-Optic Cable
* Core
* Cladding
* Buffer
* Strengthener
* Outer Jacket

<b>multimode fiber</b>, characterized by the fact that the cable allows for multiple angles (modes) of light waves entering the core.
<b>single-mode fiber</b> uses a smaller-diameter core, around one-fifth the diameter of common multimode cables. To transmit light into a much smaller core, a
laser-based transmitter sends light at a single angle (hence the name single-mode).

10 Gigabit Ethernet over Fiber allow for distances up to 400m, which would often allow for connection of devices in different buildings in the same office park. Single-mode allows dis-
tances into the tens of kilometers, but with slightly more expensive SFP/SFP+ hardware.

|Criteria|UTP|Multimode|Single-Mode|
|---|---|---|---|
|Cost of Cabling|Low|Medium|Medium|
|Cost of a Switch Port|Low|Medium|High|
|Max Distance|100m|500m|40km|
| Susceptibility to Interference|Some|None|None|
| Risk of Copying from Cable Emissions|Some|None|None|

## Sending Data in Ethernet Networks
### Ethernet Frame Format
|Field|Bytes|Descryption|
|---|---|---|
|Preamble|7|Synchronization.|
|Start Frame Delimiter (SFD)|1|Signifies that the next byte begins the Destination MAC Address field.|
|Destination MAC Address|6|Identifies the intended recipient of this frame.|
|Source MAC Address|6|Identifies the sender of this frame.|
|Type|2|Defines the type of protocol listed inside the frame; today, most likely identifies IP version 4 (IPv4) or IP version 6 (IPv6).|
|Data and Pad*|46-1500|Holds data from a higher layer, typically an L3PDU (usually an IPv4 or IPv6 packet). The sender adds padding to meet the minimum length requirement for this field (46 bytes)|
|Frame Check Sequence (FCS)|4|Provides a method for the receiving NIC to determine whether the frame experienced transmission errors.|

Media Access Control (MAC) addresses, are 6-byte-long (48-bit-long) binary numbers. The manufacturer agrees to give all NICs (and other Ethernet products) a MAC address that begins with its assigned 3-byte OUI(organizationally unique identifier). The manufacturer also assigns a unique value for the last 3 bytes, a number that manufacturer has never used with that OUI. 

* Unicast Address 
* Broadcast address: Frames sent to this address should be delivered to all devices on the Ethernet LAN. It has a value of FFFF.FFFF.FFFF. 
* Multicast addresses: Frames sent to a multicast Ethernet address will be copied and forwarded to a subset of the devices on the LAN that volunteers to receive frames sent to a specific multicast address.

#### Ethernet Type Field
* IPv4 : Type = 0800
* IPv6 : Type = 86DD
#### Error Detection with FCS
<b>error detection</b> does not also mean <b>error recovery</b>. Ethernet defines that the errored frame should be discarded, but Ethernet does not attempt to recover the lost frame. Other pro-
tocols, notably TCP, recover the lost data by noticing that it is lost and sending the data again.

####  Switches and Hubs
modern switches allows the use of full-duplex logic, which is much faster and simpler than half-duplex logic, which is required when using hubs.

* <b>Half duplex</b>: The device must wait to send if it is currently receiving a frame; in other words, it cannot send and receive at the same time. 
* <b>Full duplex</b>: The device does not have to wait before sending; it can send and receive at
the same time.

Hubs : physical layer standards rather than data-link standards and are therefore considered to be Layer 1 devices. When an electrical signal comes in one hub port, the hub repeats that electrical signal out all other ports (except the incoming port). The hub repeats all received electrical signals, even if it receives multiple signals at the same time, thus causing collisions. 

Carrier sense multiple access with collision detection (CSMA/CD)
* Listens until the Ethernet is not busy.
* Begin sending the frame
* Sender listens while sending to discover whether a collision occurs; collisions might be caused by many reasons, including unfortunate timing. If a colli- sion occurs, all currently sending nodes do the following: 
  - send a jamming signal that tells all nodes that a collision happened.
  - independently choose a random time to wait before trying again, to avoid unfortunate timing.