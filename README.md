# Zabbix Monitoring Stack with MySQL and Grafana

This repository contains a Docker Compose configuration to set up a complete Zabbix monitoring environment. It includes the Zabbix Server, Zabbix Frontend, MySQL, Grafana, and Zabbix Agent, all orchestrated via Docker containers.

## Table of Contents

- [Overview](#overview)
- [Services](#services)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Volumes](#volumes)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)

## Overview

This setup provides a robust monitoring solution with the following components:
- **Zabbix Server**: Central component for monitoring.
- **Zabbix Frontend**: Web interface for managing and viewing monitoring data.
- **MySQL**: Database for storing Zabbix data.
- **Grafana**: Advanced dashboarding and visualization for Zabbix data.
- **Zabbix Agent**: Collects metrics from the host machine and sends them to the Zabbix Server.

## Services

### MySQL
- **Image**: `mysql:8.0`
- **Ports**: `3306:3306`
- **Volumes**: `./zabbix/mysql:/var/lib/mysql`
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`
  - `MYSQL_DATABASE`
  - `MYSQL_USER`
  - `MYSQL_PASSWORD`

### Zabbix Server
- **Image**: `zabbix/zabbix-server-mysql:ubuntu-6.0-latest`
- **Ports**: `10051:10051`
- **Volumes**: `./zabbix/alertscripts:/usr/lib/zabbix/alertscripts`
- **Depends on**: `mysql`

### Zabbix Frontend
- **Image**: `zabbix/zabbix-web-apache-mysql:ubuntu-6.0-latest`
- **Ports**: `80:8080`, `443:8443`
- **Depends on**: `mysql`

### Grafana
- **Image**: `grafana/grafana:latest`
- **Ports**: `3000:3000`
- **Depends on**: `mysql`, `zabbix-server`

### Zabbix Agent
- **Image**: `zabbix/zabbix-agent2:alpine-6.0-latest`
- **Ports**: `10050:10050`
- **Depends on**: `zabbix-server`

## Prerequisites

- Docker installed on your machine.
- Docker Compose installed.


