#### **Overview

[[Internet Network Flow.canvas|Internet Network Flow]] components connects each other and performance.
1. [[#**Hub|Hub]]
2. [[#Switch|Switch]]
3. Router
4. Firewall
5. Gateway
6. Modem
7. Fiber
8. Outside Network or Internet

#### **Hub
- Hub is get connected with multiple computers and devices together,  whenever the Signal or message from source ip it broadcast to all the connected devices get back from only destination Ip's devices, and it's not store that ip and mac address of the devices. This happens every time.

MAC Address of the devices.

```mermaid
graph LR
    c1[Computer1] -->|Send message to <br> Computer4| H[Hub]
    H -->|Broadcast| c2[Computer2]
    H -->|Broadcast| c3[Computer3]
    H -->|Broadcast| c4[Computer4]
    
    c4 -->|Replied| H
     H --> |Replied| c1[Computer1]
    
    style c1 fill:#ffebee
    style c4 fill:#e8f5e8
```

#### **Switch
- It's more likes HUB but it has brained, so it's stores the mac address of the device in **CAM 
(Content Addressable Memory)** table.
- Steps and procedure of the switch
	1. A device want to sent message or ping another device in same subnet or different subnet. It get convert into ARP(Address Resolver Protocol) Packets and sent to switch.
	2. Switch received the ARP packets checks the CAM(Content Addressable Memory) table to find the mac address of the device. If it exist send message to device.
	3. If not available switch broadcast to connected device to get mac address, even if it router also.
	4. When the Ip exist the system its returns the ip and mac address to switch.
	5. Now, switch stores the ip and mac address, and returns message or ping response to source system.

	#### **Notes
	1.  Switch only perform mac address not ip address.
	2. It's a 2nd network layer.
	3. There three reason switch broadcast,
		1. When destination's mac address does not known.
		2. When Multicast get involved.
		3. When APR sends to broadcast mac address to switch.
	4. We can connect multiple switch in same environment.
	5. Ask doubt, single switch can support subnet or not? Yes


```mermaid copy
graph TD
    c1[Computer1] -->|Send message to <br> Computer4| A[ARP Request Packet]
    A --> CAM[Switch Receives Packet]
    CAM --> CT{Check CAM Table<br/>MAC of Computer4?}
    
    CT -->|Present| F[Forward to Computer4's Port]
    CT -->|Not Present| H[Broadcast ARP Request]
    
    F --> c4[Computer4]
    H -->|Broadcast| c2[Computer2]
    H -->|Broadcast| c3[Computer3]
    H -->|Broadcast| c4[Computer4]
    
    c2 -->|Not my IP| D1{Drop Packet}
    c3 -->|Not my IP| D2{Drop Packet}
    c4 -->|My IP!| R[Prepare ARP Reply]
    
    D1 -->|End| E1[End]
    D2 -->|End| E2[End]
    
    R -->|Send ARP Reply| H2[Switch]
    H2 -->|Learn MAC & Update CAM| LU[Update CAM Table]
    LU -->|Forward to Computer1| c1
    
    style c1 fill:#ffebee
    style c4 fill:#e8f5e8
    style R fill:#e8f5e8
    style CT fill:#fff3e0
    style LU fill:#e3f2fd
```

#### **Router
- Router passthrough the ip to neighbour network or firewall or internet based on configuration.
- It also use broadcast when DHCP (Dynamic Host Configuration Protocol) does not knows ip.
 #### **Responsibilities
 1. Forward request to neighbour subnet/network.
 2. 

// Todo future.....

#### **Load balancing
``` mermaid
flowchart TD
    subgraph A [Client Tier]
        C1[User Browser]
        C2[Mobile App]
        C3[API Client]
    end

    subgraph B [Layer 1: Global Load Balancer]
        GSLB[Global Server<br>Load Balancer<br>DNS/GSLB]
    end

    subgraph C [Web Tier]
        LB1[L7/HTTP Load Balancer]
        
        subgraph WebServers
            WS1[Web Server 1<br>NGINX/Apache]
            WS2[Web Server 2<br>NGINX/Apache]
            WS3[Web Server N...]
        end
    end

    subgraph D [Application Tier]
        LB2[L4/TCP Load Balancer]
        
        subgraph AppServers
            AS1[App Server 1<br>Node.js/Java]
            AS2[App Server 2<br>Node.js/Java]
            AS3[App Server N...]
        end
    end

    subgraph E [Data Tier]
        LB3[Database Proxy/LB]
        
        subgraph Databases
            PRIMARY[("Primary DB<br>Read/Write")]
            REPLICA1[("Replica 1<br>Read Only")]
            REPLICA2[("Replica 2<br>Read Only")]
        end
    end

    A --> GSLB
    GSLB --> LB1
    LB1 --> WS1
    LB1 --> WS2
    LB1 --> WS3
    
    WS1 --> LB2
    WS2 --> LB2
    WS3 --> LB2
    
    LB2 --> AS1
    LB2 --> AS2
    LB2 --> AS3
    
    AS1 --> LB3
    AS2 --> LB3
    AS3 --> LB3
    
    LB3 --> PRIMARY
    LB3 --> REPLICA1
    LB3 --> REPLICA2
```



