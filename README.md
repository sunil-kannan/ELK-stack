# ELK Stack Setup with Docker

This repository contains the setup files for running the ELK stack (Elasticsearch, Logstash, and Kibana) using Docker. The setup includes configurations for reading data from a PostgreSQL database and loading it into Elasticsearch.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

### 1. Clone the Repository

```sh
git clone https://github.com/sunil-kannan/ELK-stack.git
cd ELK-stack


elk-docker-setup/
├── docker-compose.yml
├── logstash.conf
├── goldhubBuyer_template.json
├── postgresql-42.2.29.jar
├── shakespeare_part1.json
├── shakespeare_part2.json
├── shakespeare_part3.json
└── shakespeare_part4.json
```

### 2. Database Configuration
```sh
Update the database configuration in the logstash.conf file with your own database details.


```
### 3. Download postgresql jar file
```sh
Download the PostgreSQL jar file from the PostgreSQL website. If you need a different version, make sure to update the version in the docker-compose file accordingly.

```
### 4. Run docker compose
```sh
docker-compose up -d
After running the command, you can access Kibana at http://localhost:5601/








