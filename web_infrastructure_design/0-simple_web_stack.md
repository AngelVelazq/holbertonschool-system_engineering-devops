```mermaid
graph TD
    A[User] --> B[www.foobar.com]
    B --> C[DNS \((www.foobar.com)\) --> 8.8.8.8]
    C --> D[Server (8.8.8.8)]
    D --> E[Nginx Web Server]
    E --> F[Application Server]
    F --> G[Application Files (Codebase)]
    F --> H[MySQL Database]
