## **Network Layers**

- [**Network Layers**](#network-layers)
  - [**Sources**](#sources)
  - [**Overview of TCP and UDP**](#overview-of-tcp-and-udp)
  - [**Differences between TCP and UDP**](#differences-between-tcp-and-udp)
  - [**TCP in more detail**](#tcp-in-more-detail)
  - [**Network layers and OCI model**](#network-layers-and-oci-model)

### **Sources**
- [TCP and UDP differences](https://www.youtube.com/watch?v=ddM9AcreVqY)
- [How TCP and UDP works](https://www.youtube.com/watch?v=FfvUxw8DHb0)
- [Establishing connection with TCP - 3 way handshake](https://www.youtube.com/watch?v=fQC4v07gs5k)
- [How TCP handles errors](https://www.youtube.com/watch?v=NaEHwrRHfqk)
- [Network layer & OSI model](https://www.youtube.com/watch?v=kCuyS7ihr_E)

### **Overview of TCP and UDP**
- <ins>Communication</ins>
  - Communication between 2 computers need to be good and reliable, to guarantee data is received correctly (intact & in-order).
- <ins>TCP (Transmissions control protocol)</ins>
  - Used to guarantee that all data is received in-order
  - Information sent w/o TCP may be out of order
  - Connection oriented protocol - must first acknowledge a session between the 2 computers before a connection takes place
  - Connection established via a 3-way handshake
      - Sender sends a send message - SYN
      - Receiver sends back confirmation of receipt - SYN ACK
      - Sender sends an acknowledgement - ACK RECEIVED
  - After established - only data can be delivered
  - TCP guarantees delivery of data
    - If data packet is 'dropped', TCP will resend it
- <ins>UDP (User Datagram Protocol)</ins>
  - Connnectionless oriented protocol
    - Does not establish a 'session'
    - Does not guarantee data delivery
  - Sending data
    - When sender sends data, it doesn't care if data is received on the other end 
    - UDP also known as 'Fire and forget' protocol
  - vs TCP
    - less overhead to guarantee data delivery and establishing a session
    - will be faster than TCP

### **Differences between TCP and UDP**
| TCP                                                                          | UDP                                                                                                                                          |
|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Packets</br> - Additional Features (20 to 60 bytes per packet)                    | Lightweight (only 8 bytes)                                                                                                                   |
| Connection oriented                                                          | Connectionless                                                                                                                               |
| Error recovery                                                               | Does not care about errors                                                                                                                   |
| Ordered Data Delivery                                                        | Order not prioritised                                                                                                                        |
| More overhead</br> - acknowledgement of session</br> - guarantee data delivery | Less overhead</br> - does not have similar features                                                                                               |
| Windowing (Flow Control)                                                     |                                                                                                                                              |
| Most applications                                                               | Use for real time applications</br> - voice/video streaming (no retransmission required)</br> - sending DNS (which can re-arrange the data themselves) |
|                                                                              |                                                                                                                                              |

### **TCP in more detail**
- 3 Way handshake
  - Flags in packet headers are turned off and on when transmitting between devices
  - Same as above - SYN or ACK will be turned on
  - Initialisation of packet headers
    - Port numbers (sorce & destination ports)
    - ISN (initial Sequence number)
    - Window size
- Closing connections (2 methods)
  - This is more graceful method, and there are 4 messages
    - Either devices will send FIN/ACK flags on, other device will send ACK message
    - Corresponding device will send FIN/ACK again and other device ACK
  - Non graceful method
    - one device sends with the RST (reset) flag
    - connection would just drop immediately
    - RST messages are only sent if there errors, i.e. for troubleshooting
- Error recovery
  - Use sequence and acknowledgement headers in packets to track sequence of loss packets
  - Windows size (buffer) to receive information before checking any errors of packet losses, and retransmission
    - When initialised during the 3 way handshake, the window size will NOT stay static
    - It may become dynamic, depending on the stability of the connections, e.g. slowly 8kb -> 16kb -> 32kb
  - Resending information
    - if packet 4/10 is dropped, the sender will usually re-send packets 4 to 10 again
    - So, larger window sizes may result in larger transmission overhead
    - If connections become less stable, window size may shrink, e.g. 16kb -> 8kb

### **Network layers and OCI model**
- OCI (Open systems interconnect) model
  - This is a theoretical/conceptual model, it was never implemented
  - What we actually have is the TCP/IP model and they have their own 'Data units'
    - Packets can also be called 'Datagrams'
  - Representations as 'Devices
    - Layer 1 - layer of the wire - fibre optics/copper cables/WAP
    - Layer 2 - more specific to a switch 
- 7 layers (Pls do not throw sausage pizza away)
  - Application
  - Presentation
  - Sessions
  - Transport - TCP/UDP layer
  - Network - IP layer
  - Data link - 
  - Physical