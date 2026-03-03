# SonarQube Software Configuration  
## Ansible Role Documentation & POC Setup Guide  

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---
# Table of Contents

1. [Introduction](#1-introduction)
   - [What is SonarQube?](#what-is-sonarqube)

2. [Objective of This Document](#2-objective-of-this-document)

3. [Why SonarQube?](#3-why-sonarqube)

4. [Why Ansible for SonarQube Setup?](#4-why-ansible-for-sonarqube-setup)
   - [What is Ansible?](#what-is-ansible)

5. [SonarQube Architecture Overview](#5-sonarqube-architecture-overview)

6. [System Requirements](#6-system-requirements)

7. [Ansible Role Structure](#7-ansible-role-structure)

8. [Role Variables (defaults/main.yml)](#8-role-variables-defaultsmainyml)

9. [Installation Tasks (tasks/install.yml)](#9-installation-tasks-tasksinstallyml)

10. [Configuration Tasks (tasks/configure.yml)](#10-configuration-tasks-tasksconfigureyml)

11. [Service Configuration](#11-service-configuration)

12. [Handlers](#12-handlers)

13. [Deployment Workflow](#13-deployment-workflow)

14. [POC – Manual SonarQube Setup (Without Ansible)](#14-poc--manual-sonarqube-setup-without-ansible)
   - [Step 1: Install Java](#step-1-install-java)
   - [Step 2: Install PostgreSQL](#step-2-install-postgresql)
   - [Step 3: Download SonarQube](#step-3-download-sonarqube)
   - [Step 4: Configure Database](#step-4-configure-database)
   - [Step 5: Start SonarQube](#step-5-start-sonarqube)
   - [Step 6: Access UI](#step-6-access-ui)

15. [Security Best Practices](#15-security-best-practices)

16. [Monitoring Recommendations](#16-monitoring-recommendations)

17. [Advantages of Using Ansible Role](#17-advantages-of-using-ansible-role)

18. [Conclusion](#18-conclusion)

19. [References](#19-references)

20. [Contact Information](#20-contact-information)

---

# 1. Introduction

## What is SonarQube?

**SonarQube** is an open-source platform used for continuous inspection of code quality. It performs:

- Static Code Analysis  
- Bug Detection  
- Code Smell Identification  
- Security Vulnerability Scanning  
- Code Coverage Reporting  
- Quality Gate Enforcement  

It integrates seamlessly with CI/CD tools like:

- Jenkins  
- GitHub  
- GitLab  

---

# 2. Objective of This Document

This document provides:

- Detailed explanation of SonarQube
- Complete Ansible role structure documentation
- Step-by-step explanation of each configuration
- Best practices
- Manual POC setup (for validation before automation)
- Production recommendations

Note: This document covers documentation only. Implementation will be done in the next sprint.

---

# 3. Why SonarQube?

| Problem | Solution with SonarQube |
|----------|-------------------------|
| Poor code quality | Automated static analysis |
| Security vulnerabilities | Security hotspot detection |
| No coding standards | Enforced quality rules |
| No quality validation | Quality Gate in CI/CD |
| Technical debt | Technical debt measurement |

---

# 4. Why Ansible for SonarQube Setup?

## What is Ansible?

Ansible is an automation tool used for:

- Configuration management
- Infrastructure as Code (IaC)
- Software provisioning
- Server automation

### Benefits of Using Ansible Role

| Manual Setup | Ansible Role |
|--------------|--------------|
| Time consuming | Automated |
| Error-prone | Consistent |
| Not reusable | Reusable |
| Hard to scale | Easily scalable |

---

# 5. SonarQube Architecture Overview

<img width="900" height="525" alt="image" src="https://github.com/user-attachments/assets/7aa809c9-7e8e-4863-b0ee-ac14881d7f70" />


### Core Components:

1. SonarQube Server  
2. PostgreSQL Database  
3. Sonar Scanner  
4. Web UI  
5. Reverse Proxy (Optional – NGINX)

---

# 6. System Requirements

## Hardware

| Component | Minimum Requirement |
|------------|--------------------|
| RAM | 4GB (8GB Recommended) |
| CPU | 2 Core |
| Disk | 10GB |

## Software

- Linux (Ubuntu/CentOS)
- Java 17
- PostgreSQL 13+

---

# 7. Ansible Role Structure

```
roles/
  sonarqube/
    defaults/
      main.yml
    vars/
      main.yml
    tasks/
      main.yml
      install.yml
      configure.yml
      service.yml
    templates/
      sonar.properties.j2
    handlers/
      main.yml
    files/
    meta/
      main.yml
```

---

# 8. Role Variables (defaults/main.yml)

```yaml
sonarqube_version: "10.4.0"
sonarqube_user: "sonar"
sonarqube_group: "sonar"
sonarqube_port: 9000
sonarqube_db_name: "sonarqube"
sonarqube_db_user: "sonar"
sonarqube_db_password: "sonar123"
```

Why?

- Makes role reusable
- Allows environment-based overrides
- Keeps configuration flexible

---

# 9. Installation Tasks (tasks/install.yml)

Responsibilities:

- Install Java
- Create SonarQube user
- Download SonarQube
- Extract package
- Set ownership and permissions

Example:

```yaml
- name: Install Java
  apt:
    name: openjdk-17-jdk
    state: present
```

---

# 10. Configuration Tasks (tasks/configure.yml)

Template: `templates/sonar.properties.j2`

```properties
sonar.jdbc.username={{ sonarqube_db_user }}
sonar.jdbc.password={{ sonarqube_db_password }}
sonar.jdbc.url=jdbc:postgresql://localhost/{{ sonarqube_db_name }}
sonar.web.port={{ sonarqube_port }}
```

Why use template?

- Dynamic configuration
- Environment-based DB configuration
- Clean separation of logic & config

---

# 11. Service Configuration

Systemd file location:

```
/etc/systemd/system/sonarqube.service
```

Enable service:

```yaml
- name: Enable SonarQube
  systemd:
    name: sonarqube
    enabled: yes
    state: started
```

---

# 12. Handlers

```yaml
- name: restart sonarqube
  systemd:
    name: sonarqube
    state: restarted
```

Purpose:

- Restart service when configuration changes
- Maintains idempotency

---

# 13. Deployment Workflow

```
Developer → Push Code → CI Pipeline → Sonar Scanner → SonarQube Server → Database
                                            ↓
                                     Quality Gate Result
```

---

# 14. POC – Manual SonarQube Setup (Without Ansible)

## Step 1: Install Java

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
<img width="1805" height="159" alt="image" src="https://github.com/user-attachments/assets/d1f4be1a-814a-48a8-a2bb-512a01129b7a" />


---

## Step 2: Install PostgreSQL

```bash
sudo apt install postgresql postgresql-contrib -y
```
verify:
```bash
psql --version
```
<img width="1380" height="126" alt="image" src="https://github.com/user-attachments/assets/af4bdfa7-a759-4f8e-b076-31e275790e51" />


Create Database:

```bash
sudo -u postgres psql
CREATE DATABASE sonarqube;
CREATE USER sonar WITH ENCRYPTED PASSWORD 'sonar123';
GRANT ALL PRIVILEGES ON DATABASE sonarqube TO sonar;
GRANT ALL ON SCHEMA public TO sonar;
ALTER SCHEMA public OWNER TO sonar;
\q
```
<img width="1854" height="886" alt="image" src="https://github.com/user-attachments/assets/d88db648-1540-4821-9d64-98e850dfc488" />


---

## Step 3: Download SonarQube

```bash
cd /opt
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.5.1.90531.zip
sudo unzip sonarqube-10.5.1.90531.zip
sudo mv sonarqube-10.5.1.90531 sonarqube
sudo chown -R sonar:sonar /opt/sonarqube
```

---

## Step 4: Configure Database

Edit:

```
sudo nano /opt/sonarqube/conf/sonar.properties
```

Update:

```
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar123
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
```
<img width="1810" height="403" alt="image" src="https://github.com/user-attachments/assets/a9f9707e-cc15-4c41-b446-18db64403452" />


---

## Step 5: Start SonarQube

```bash
sudo -u sonar /opt/sonarqube/bin/linux-x86-64/sonar.sh start
```
<img width="1851" height="493" alt="image" src="https://github.com/user-attachments/assets/493e08ee-359c-4106-af7b-6f8158f349ce" />


---

## Step 6: Access UI

```
http://localhost:9000
```
<img width="1500" height="700" alt="image" src="https://github.com/user-attachments/assets/eddb5a9b-48b7-4ee1-bbad-f5e2ab6f3292" />


Default Credentials:

```
admin / admin
```

---

# 15. Security Best Practices

- Change default admin password
- Use HTTPS with NGINX reverse proxy
- Secure DB credentials using Ansible Vault
- Restrict firewall access
- Disable public anonymous access
- Use LDAP/SSO for enterprise

---

# 16. Monitoring Recommendations

Monitor:

- CPU usage
- Memory consumption
- JVM heap usage
- Database connections
- Disk space

Recommended Tools:

- Prometheus
- Grafana
- ELK Stack

---

# 17. Advantages of Using Ansible Role

| Feature | Benefit |
|----------|---------|
| Automation | Faster deployments |
| Idempotency | Safe multiple runs |
| Reusability | Multi-environment support |
| Version control | Git-based infra |
| Scalability | Production-ready |

---

# 18. Conclusion

For Production:

- Use PostgreSQL
- Use Reverse Proxy (NGINX)
- Enable HTTPS
- Monitor JVM and DB
- Secure credentials with Vault
- Implement via Ansible Role

### Recommended Approach

1. Validate via Manual POC
2. Develop Reusable Ansible Role
3. Integrate with CI/CD
4. Apply Security Hardening
5. Move to Production

---

# 19. References

| Component                      | Description                                                                    | Official Link                                                                                                                                                          |
| ------------------------------ | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SonarQube Documentation        | Complete setup, configuration, upgrade, and administration guide for SonarQube | [https://docs.sonarsource.com/sonarqube/latest/](https://docs.sonarsource.com/sonarqube/latest/)                                                                       |
| SonarQube Download Page        | Download Community, Developer, Enterprise editions                             | [https://www.sonarqube.org/downloads/](https://www.sonarqube.org/downloads/)                                                                                           |
| SonarQube System Requirements  | Hardware, OS, Java, DB requirements                                            | [https://docs.sonarsource.com/sonarqube/latest/requirements/system-requirements/](https://docs.sonarsource.com/sonarqube/latest/requirements/system-requirements/)     |
| Ansible Documentation          | Official Ansible automation and role development documentation                 | [https://docs.ansible.com/](https://docs.ansible.com/)                                                                                                                 |
| Ansible Role Development Guide | Best practices for creating reusable Ansible roles                             | [https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html) |
| PostgreSQL Documentation       | Official PostgreSQL administration and SQL reference                           | [https://www.postgresql.org/docs/](https://www.postgresql.org/docs/)                                                                                                   |
| PostgreSQL Role & Privileges   | Managing database users, schema permissions                                    | [https://www.postgresql.org/docs/current/sql-grant.html](https://www.postgresql.org/docs/current/sql-grant.html)                                                       |
| Java 17 Documentation          | OpenJDK installation and configuration                                         | [https://openjdk.org/projects/jdk/17/](https://openjdk.org/projects/jdk/17/)                                                                                           |

---

# 20. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) | 

---
