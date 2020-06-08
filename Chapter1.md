> https://www.cs.ait.ac.th/~on/O/oreilly/tcpip/tcpip/ch01_01.htm

> Chapter 1: Overview of TCP/IP

**Networking computers dramatically enhances their ability to communicate - and most computers are used more for communication than computation.**

> Objective/Summary 

- Discuss TCP/IP, the protocol suite upon which the Internet is built and it's structure.

- See TCP/IP hierarchy of four layers: Applications, Host-to-Host Transport, Internet, and Network Access. 

- Examine the function of each of these layers. 


### 1.2 A Data Communications Model
Packet switching is a method of grouping data that is transmitted over a digital network into packets. Packets are made of a header and a payload. Data in the header is used by networking hardware to direct the packet to its destination where the payload is extracted and used by application software.Wikipedia
In 1969 the Advanced Research Projects Agency (ARPA) funded a research and development project to create an experimental packet-switching network ARPANET.
Protocols are formal rules of behavior. In international relations, protocols minimize the problems caused by cultural differences when various nations work together. By agreeing to a common set of rules that are widely known and independent of any nation's customs, diplomatic protocols minimize misunderstandings; everyone knows how to act and how to interpret the actions of others. Similarly, when computers communicate, it is necessary to define a set of rules to govern their communications.
Most information about TCP/IP protocols is published as Requests for Comments (RFCs)
As a network system administrator, you will no doubt read many of the RFCs yourself. Some contain practical advice and guidance that is simple to understand. Other RFCs contain protocol implementation specifications defined in terminology that is unique to data communications.
Open Systems Interconnect (OSI) model provides a common reference for discussing communications. The terms defined by this model are well understood and widely used in the data communications community - so widely used, in fact, that it is difficult to discuss data communications without using OSI's terminology.

How information is transmitted in layers
![image](https://user-images.githubusercontent.com/414141/82076763-03edd800-96fe-11ea-9e14-cde8d21b4da8.png)

The **Application Layer** is the level of the protocol hierarchy where user-accessed network processes reside. In this text, a TCP/IP application is any network process that occurs above the Transport Layer. This includes all of the processes that users directly interact with, as well as other processes at this level that users are not necessarily aware of.
For cooperating applications to exchange data, they must agree about how data is represented. In OSI, **Presentation Layer** provides standard data presentation routines. This function is frequently handled within the applications in TCP/IP, though increasingly TCP/IP protocols such as External Data Representation (XDR) and Multipurpose Internet Mail Extensions (MIME) perform this function.

As with the Presentation Layer, the **Session Layer** is not identifiable as a separate layer in the TCP/IP protocol hierarchy. This manages the sessions (connection) between cooperating applications. In TCP/IP, this function largely occurs in the Transport Layer, and the term "session" is not used. For TCP/IP, the terms "socket" and "port" are used to describe the path over which cooperating applications communicate.

Much of our discussion of TCP/IP is directed to the protocols that occur in the **Transport Layer**. _This layer guarantees that the receiver gets the data exactly as it was sent_. In TCP/IP this function is performed by the Transmission Control Protocol (TCP). However, TCP/IP offers a second Transport Layer service, User Datagram Protocol (UDP), that does not perform the end-to-end reliability checks.

The **Network Layer** manages connections across the network and isolates the upper layer protocols from the details of the underlying network. The Internet Protocol (IP), which isolates the upper layers from the underlying network and handles the addressing and delivery of data, is usually described as TCP/IP's Network Layer.
The reliable delivery of data across the underlying physical network is handled by the **Data Link Layer**. TCP/IP rarely creates protocols in the Data Link Layer. Most RFCs that relate to the Data Link Layer discuss how IP can make use of existing data link protocols.

The **Physical Layer** defines the characteristics of the hardware needed to carry the data transmission signal. Features such as voltage levels, and the number and location of interface pins, are defined in this layer. Examples of standards at the Physical Layer are interface connectors such as RS232C and V.35, and standards for local area network wiring such as IEEE 802.3. TCP/IP does not define physical standards - it makes use of existing standards.


### 1.3 TCP/IP Protocol Architecture
Each layer in the stack adds control information to ensure proper delivery. This control information is called a header because it is placed in front of the data to be transmitted. Each layer treats all of the information it receives from the layer above as data and places its own header in front of that information. The addition of delivery information at every layer is called encapsulation. (See Figure 1.3 for an illustration of this.) When data is received, the opposite happens. Each layer strips off its header before passing the data on to the layer above.
Applications using TCP refer to data as a stream, while applications using the User Datagram Protocol (UDP) refer to data as a message. TCP calls data a segment, and UDP calls its data structure a packet. The Internet layer views all data as blocks called datagrams. TCP/IP uses many different types of underlying networks, each of which may have a different terminology for the data it transmits. Most networks refer to transmitted data as packets or frames.
Each layer has its own independent data structures. Conceptually, a layer is unaware of the data structures used by the layers above and below it. In reality, the data structures of a layer are designed to be compatible with the structures used by the surrounding layers for the sake of more efficient data transmission. Still, each layer has its own data structure and its own terminology to describe that structure.


### 1.4 Network Access Layer
Network Access Layer can encompass the functions of all three lower layers of the OSI reference Model (Network, Data Link, and Physical). The protocols in this layer provide the means for the system to deliver data to the other devices on a directly attached network. It defines how to use the network to transmit an IP datagram. Unlike higher-level protocols, Network Access Layer protocols must know the details of the underlying network (its packet structure, addressing, etc.) to correctly format the data being transmitted to comply with the network constraints.
The design of TCP/IP hides the function of the lower layers, and the better known protocols (IP, TCP, UDP, etc.) are all higher-level protocols.
Functions performed at this level include encapsulation of IP datagrams into the frames transmitted by the network, and mapping of IP addresses to the physical addresses used by the network.
Protocols in this layer often appear as a combination of device drivers and related programs

### 1.5 Internet Layer
The **Internet Protocol** is the building block of the Internet. Its functions include:
- Defining the datagram, which is the basic unit of transmission in the Internet
- Defining the Internet addressing scheme
- Moving data between the Network Access Layer and the Host-to-Host Transport Layer
- Routing datagrams to remote hosts
- Performing fragmentation and re-assembly of datagrams
It accurately deliver your data to the connected network. It is a connectionless protocol so relies on protocols in other layers to establish the connection if they require connection-oriented service. Further it relies in the other layers to provide error detection and error recovery.

IP datagram format
![image](https://user-images.githubusercontent.com/414141/82591158-a1458200-9bbe-11ea-8b71-f1afbd1dba00.png)

**Internet Gateways** (or also called as IP routers) routing packets between networks
![image](https://user-images.githubusercontent.com/414141/82591351-ef5a8580-9bbe-11ea-99c6-cf86485b7614.png)
Each type of network has a **maximum transmission unit (MTU)**, which is the largest packet that it can transfer. If the datagram received from one network is longer than the other network's MTU, it is necessary to divide the datagram into smaller fragments for transmission. This process is called fragmentation. an Ethernet is physically different from an X.25 network; IP must break an Ethernet's relatively large packets into smaller packets before it can transmit them over an X.25 network.

An integral part of IP is the **Internet Control Message Protocol (ICMP)** which uses the IP datagram delivery facility to send its messages. _ICMP sends messages that perform the following control, error reporting, and informational functions_ for TCP/IP.

- Flow control: When datagrams arrive too fast for processing, the destination host or an intermediate gateway sends an ICMP Source Quench Message back to the sender. This tells the source to stop sending datagrams temporarily.
- Detecting unreachable destinations: When a destination is unreachable, the system detecting the problem sends a Destination Unreachable Message to the datagram's source. If the unreachable destination is a network or host, the message is sent by an intermediate gateway. But if the destination is an unreachable port, the destination host sends the message.
- Redirecting routes: A gateway sends the ICMP Redirect Message to tell a host to use another gateway, presumably because the other gateway is a better choice. This message can be used only when the source host is on the same network as both gateways.
- Checking remote hosts: A host can send the ICMP Echo Message to see if a remote system's Internet Protocol is up and operational. When a system receives an echo message, it replies and sends the data from the packet back to the source host. The ping command uses this message.


### 1.6 Transport Layer (or  Host-to-Host Transport Layer)
The two most important protocols in this layer:
  - Transmission Control Protocol (TCP)
    TCP provides **connection-oriented** reliable data delivery service with end-to-end error detection and correction. 
  - User Datagram Protocol (UDP)
    UDP provides low-overhead, **connectionless** datagram delivery service. 

Both protocols deliver data between the Application Layer and the Internet Layer. Applications programmers can choose whichever service is more appropriate for their specific applications.

UDP message format
![image](https://user-images.githubusercontent.com/414141/82676403-13bd6d00-9c66-11ea-9ac6-469cf3674ce7.png)

TCP segment format
![image](https://user-images.githubusercontent.com/414141/82677068-297f6200-9c67-11ea-8f9a-faa6c3927f91.png)

Why do applications programmers choose UDP as a data transport service?  
If the amount of data being transmitted is small, the overhead of creating connections and ensuring reliable delivery may be greater than the work of re-transmitting the entire data set. Example, query-response model.
Applications that require the transport protocol to provide reliable data delivery use TCP because it verifies that data is delivered across the network accurately and in the proper sequence. TCP is a _reliable_, _connection-oriented_, _byte-stream_ protocol.
It provides reliability with a mechanism called Positive Acknowledgment with Re-transmission (PAR). Simply stated, a system using PAR sends the data again, unless it hears from the remote system that the data arrived okay. A logical end-to-end connection between the two communicating hosts is established.

Three-way handshake in TCP
![image](https://user-images.githubusercontent.com/414141/82677651-14ef9980-9c68-11ea-98af-d2268c8de35a.png)

TCP data stream
![image](https://user-images.githubusercontent.com/414141/82678011-9d6e3a00-9c68-11ea-953a-1d49c02a7c7f.png)


### 1.7 Application Layer
This layer includes all processes that use the Transport Layer protocols to deliver data. There are many applications protocols. Most provide user services, and new services are always being added to this layer.
The most widely known and implemented applications protocols are:
- telnet The Network Terminal Protocol, which provides remote login over the network.
- FTP The File Transfer Protocol, which is used for interactive file transfer.
- SMTP The Simple Mail Transfer Protocol, which delivers electronic mail.
- HTTP The Hypertext Transfer Protocol, which delivers Web pages over the network.

Some other commonly used TCP/IP applications are:
- Domain Name Service (DNS) 
  Also called name service, this application maps IP addresses to the names assigned to network devices. DNS is discussed in detail in this book.
- Open Shortest Path First (OSPF)
  Routing is central to the way TCP/IP works. OSPF is used by network devices to exchange routing information. Routing is also a major topic of this book.
- Network Filesystem (NFS)
  This protocol allows files to be shared by various hosts on the network.

Some protocols, such as telnet and FTP, can only be used if the user has some knowledge of the network. Other protocols, like OSPF, run without the user even knowing that they exist. As system administrator, you are aware of all these applications and all the protocols in the other TCP/IP layers. And you're responsible for configuring them!

