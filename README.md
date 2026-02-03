# VProfile Multi-Tier Web Stack (Manual Provisioning)

## Project Overview

This project documents the manual deployment of the VProfile multi-tier application in a local virtualized environment. Five VMs are provisioned to isolate each service tier, highlighting service dependencies, configuration flow, and end-to-end deployment.

## Architecture & Technology Stack

The system follows a classic multi-tier architecture where each service is isolated for scalability and security.

- **Virtualization & Orchestration:** Oracle VM VirtualBox and Vagrant.
- **Web Tier:** Nginx acting as a web server and reverse proxy.
- **Application Tier:** Apache Tomcat serving the Java application.
- **Messaging/Brokerage:** RabbitMQ for queuing and broker services.
- **Caching Layer:** Memcached for database caching.
- **Database Tier:** MySQL/MariaDB for relational data storage.

### Architecture Diagram

![Architecture Diagram](docs/images/architecture-diagram.png)

## Implementation Roadmap

The deployment order follows service dependencies so that backend services are ready before the application tier connects.

### 1) Environment Setup

Configured the vagrant-hostmanager plugin to enable VM-to-VM name resolution via hostnames instead of static IPs.

![Vagrant Status](docs/images/vagrant-status.png)

### 2) Database Provisioning (MariaDB)

Initialized the accounts database, verified schema load, and ensured port 3306 access.

![Database Tables](docs/images/database-tables.png)

![Database List](docs/images/databases-list.png)

### 3) Cache and Messaging

Configured Memcached to listen on port 11211 and validated the service startup.

![Memcached Status](docs/images/memcached-status.png)

Provisioned RabbitMQ with a dedicated administrative user and validated service status.

![RabbitMQ Status](docs/images/rabbitmq-status.png)

### 4) Application Server (Tomcat)

Installed Java 17 and Tomcat 10 on app01 and validated the Tomcat service.

![Tomcat Status](docs/images/tomcat-status.png)

### 5) Build and Deployment (Maven)

Built the application from source using Maven and deployed the generated .war into Tomcat.

![Maven Build Success](docs/images/maven-build.png)

### 6) Web Proxy Configuration (Nginx)

Configured Nginx on web01 as a reverse proxy and verified the service status.

![Nginx Status](docs/images/nginx-status.png)

## Application Screenshots

### Login Page

![Login Page](docs/images/login-page.png)

### User Dashboard

![User Dashboard](docs/images/dashboard.png)

### Users List

![Users List](docs/images/users-list.png)

### User Details (DB + Cache)

![User Details](docs/images/user-details.png)

### RabbitMQ Integration

![RabbitMQ Initiated](docs/images/rabbitmq-initiated.png)

## Key Technical Competencies Demonstrated

- **Linux Administration:** Package management, service control, and permissions.
- **Network Security:** Host-based firewall rules to secure service ports.
- **Infrastructure as Code (Intro):** Reproducible VM provisioning with Vagrant.
