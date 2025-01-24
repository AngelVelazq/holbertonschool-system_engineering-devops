```mermaid
graph TD
    A[User] --> B[www.foobar.com]
    B --> C[DNS resolves www.foobar.com to 8.8.8.8]
    C --> D[Server with IP 8.8.8.8]
    D --> E[Nginx Web Server]
    E --> F[Application Server]
    F --> G[Application Files - Codebase]
    F --> H[MySQL Database]

    subgraph Issues
        I1[SPOF - Single Point of Failure]
        I2[Downtime During Maintenance]
        I3[Scalability Limitations]
    end

    D --> I1
    D --> I2
    D --> I3
