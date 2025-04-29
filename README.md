graph TB
    subgraph "Client Layer"
        WebUI[Web UI<br/>Next.js Frontend]
        BotAgent[Bot Agent<br/>Python Automation]
    end

    subgraph "API Layer"
        Auth[Authentication Service]
        API[API Gateway<br/>ASP.NET Core]
        Tenant[Tenant Resolution]
    end

    subgraph "Application Layer"
        subgraph "Core Services"
            UserService[User Service]
            BotService[Bot Agent Service]
            PackageService[Package Service]
            ScheduleService[Schedule Service]
            ExecutionService[Execution Service]
        end

        subgraph "Infrastructure"
            Repository[Repository Layer]
            Cache[Cache Service]
            Queue[Message Queue]
        end
    end

    subgraph "Data Layer"
        DB[(Database<br/>PostgreSQL)]
        FileStorage[(File Storage<br/>Automation Packages)]
    end

    subgraph "External Systems"
        Email[Email Service]
        Notification[Notification Service]
        Monitoring[Monitoring Service]
    end

    %% Connections
    WebUI --> API
    BotAgent --> API
    API --> Auth
    API --> Tenant
    Tenant --> Core Services
    Core Services --> Repository
    Repository --> DB
    Core Services --> Cache
    Core Services --> Queue
    Core Services --> FileStorage
    Core Services --> External Systems

    %% Multi-tenant Flow
    Tenant --> DB
    Repository --> Tenant
