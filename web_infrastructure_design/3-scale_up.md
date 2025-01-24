```mermaid
flowchart TD
    User["User's Computer"]
    DNS["DNS Server\n(www.foobar.com)"]
    
    subgraph External["External Network"]
        FW1["Firewall 1"]
    end
    
    subgraph LB["Server 1: Load Balancer"]
        FW2["Firewall 2"]
        HAProxy["HAProxy\nSSL Termination"]
        MC1["Monitoring Client"]
    end
    
    subgraph WS1["Server 2: Web/Application"]
        FW3["Firewall 3"]
        Nginx["Nginx"]
        App["Application Server"]
        Code["Code Base"]
        MC2["Monitoring Client"]
    end
    
    subgraph WS2["Server 3: Database"]
        FW4["Firewall 4"]
        MySQL_Primary["MySQL Primary"]
        MySQL_Replica["MySQL Replica"]
        MC3["Monitoring Client"]
    end
    
    User <--"1. DNS Query"--> DNS
    User <--"2. HTTPS"--> FW1
    FW1 <--> HAProxy
    HAProxy <--> FW2
    FW2 <--> Nginx
    Nginx <--> App
    App <--> Code
    App <--"Encrypted Data"--> FW3
    FW3 <--"Encrypted Data"--> MySQL_Primary
    MySQL_Primary --"Replication"--> MySQL_Replica
    
    MonitoringService["Monitoring Service\n(Sumo Logic)"]
    MC1 & MC2 & MC3 --"Metrics & Logs"--> MonitoringService
