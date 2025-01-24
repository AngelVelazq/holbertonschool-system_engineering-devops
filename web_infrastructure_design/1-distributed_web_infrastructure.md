flowchart TD
    User["User's Computer"]
    DNS["DNS Server\n(www.foobar.com)"]
    
    subgraph LB["Server 1: Load Balancer (HAproxy)"]
        HAProxy["HAProxy\nRound Robin Algorithm"]
    end
    
    subgraph WS1["Server 2: Web/Application Server"]
        Nginx1["Nginx"]
        App1["Application Server"]
        Code1["Code Base"]
    end
    
    subgraph WS2["Server 3: Database Server"]
        MySQL_Primary["MySQL Primary\n(Master)"]
        MySQL_Replica["MySQL Replica\n(Slave)"]
    end
    
    User <--"1. DNS Query"--> DNS
    User <--"2. HTTP"--> HAProxy
    HAProxy <--> Nginx1
    Nginx1 <--> App1
    App1 <--> Code1
    App1 <--"Read/Write"--> MySQL_Primary
    MySQL_Primary --"Replication"--> MySQL_Replica
