# Technical Project Report: VProfile Multi-Tier Web Stack

## Project Overview

This project involves the manual deployment of a robust, multi-tier web application stack named "VProfile" in a local virtualized environment. The objective was to orchestrate five distinct Virtual Machines to handle specific architectural layers, ensuring a deep understanding of service interdependencies and manual provisioning.

## 1. Architecture & Technology Stack

The system follows a classic multi-tier architecture where each service is isolated for scalability and security.

- **Virtualization & Orchestration:** Oracle VM VirtualBox and Vagrant.
- **Web Tier:** Nginx acting as a Web Service and Reverse Proxy.
- **Application Tier:** Apache Tomcat serving as the Java Application Server.
- **Messaging/Brokerage:** RabbitMQ for queuing and broker services.
- **Caching Layer:** Memcached for database caching to optimize performance.
- **Database Tier:** MySQL/MariaDB for relational data storage.

### Architecture Diagram

![Architecture Diagram](docs/images/architecture-diagram.png)

## 2. Implementation Roadmap

The setup followed a strict dependency based order to ensure backend services were available before the application tier attempted to connect.

### Step 1: Environment Setup

Configured the vagrant-hostmanager plugin to automate host mapping, allowing the VMs to communicate via internal DNS (hostnames) instead of static IPs.

![Vagrant Status](docs/images/vagrant-status.png)

### Step 2: Backend Provisioning (DB, MC, RMQ)

#### Database:
Setup MariaDB on db01, initialized the accounts database, and configured firewall port 3306.

![Database Tables](docs/images/database-tables.png)

#### Memcached:
Configured on mc01 to listen on port 11211 and updated configuration to allow global listening.

#### RabbitMQ:
Setup on rmq01 with a dedicated "test" administrator user.

![Memcached and RabbitMQ Setup](docs/images/memcached-rabbitmq.png)

### Step 3: Application Deployment (Tomcat & Maven)

Deployed Java 17 and Tomcat 10 on app01. Built the application from source using Maven, generating a .war artifact which was then deployed to the Tomcat webapps directory.

![Maven Build Success](docs/images/maven-build.png)

### Step 4: Web Proxy Configuration

Nginx was configured on web01 as a reverse proxy. A configuration file was created to load balance and proxy requests to the Tomcat application server on port 8080.

![Nginx Configuration](docs/images/nginx-config.png)

## 3. Key Technical Competencies Demonstrated

**Linux Administration:**
Proficient in package management (dnf, apt), service handling (systemctl), and permissions.

**Network Security:**
Implementing host-based firewalls using firewalld to secure service ports.

**Infrastructure as Code (Intro):**
Using Vagrant for reproducible environment creation.

## Application Screenshots

### Final Application Login Page

![Login Page](docs/images/login-page.png)

### User Dashboard

![User Dashboard](docs/images/dashboard.png)

### Users List

![Users List](docs/images/users-list.png)

### User Details (Data from DB and Cache)

![User Details](docs/images/user-details.png)

### RabbitMQ Integration

![RabbitMQ Initiated](docs/images/rabbitmq-initiated.png)
