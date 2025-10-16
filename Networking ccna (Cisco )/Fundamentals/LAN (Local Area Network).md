#### **Overview

[[Internet Network Flow.canvas|Internet Network Flow]] components connects each other and performance.
1. [[#**Hub|Hub]]
2. Switch
3. Router
4. Firewall
5. Modem
6. Fiber
7. Outside Network or Internet

#### **Hub
Hub is get connected with multiple computers and devices together,  whenever the Signal or message from source ip it broadcast to all the connected devices which does not store the 
MAC Address of the devices.

```mermaid
graph LR
    c1[Computer1] -->|Send message to <br> Computer4| H[Hub]
    H -->|Broadcast| c2[Computer2]
    H -->|Broadcast| c3[Computer3]
    H -->|Broadcast| c4[Computer4]
    
    style c1 fill:#ffebee
    style c4 fill:#e8f5e8
```

