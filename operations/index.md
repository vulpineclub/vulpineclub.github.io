---
layout: default
title: operational resources
---

## Quick reference

- Importing custom emojo
  - Plop a tarfile containing files named `shortcode.png` in `/tmp`
  - `docker-compose run --rm -v /tmp:/mnt web tootctl emoji import /mnt/rey-emojo.tar.gz`

## Projects

- Kubernetes
- Multi-server scaling
- Multi-instance shared architecture

## System overview

### vulpine.club site

![vulpine.club architecture]({{ '/assets/images/architecture.svg' | relative_url }})

- Currently a single Linode 8GB instance (smithwicks)

#### Networks

Each container only connects to the networks it needs.

- `external_network` is the only network with Internet access
  - IPv6 is primary - `2600:3c03:e000:027b::/64`
  - IPv4 requires NAT, w/ port forwarding for inbound (🤮)
    - Hardcoded to `172.31.0.0/16` (the last /16 of that RFC 1918 range)

- `internal_network` goes between the Load Balancer and Frontend networks

- `db_network`, `es_network`, and `redis_network` are the networks for accessing PostgreSQL, ElasticSearch, and Redis respectively

#### Load Balancer

- **nginx**
  - Public IP: `2600:3c03:e000:27b::e621:10`
  - Configs: `/etc/nginx`
  - TLS certificate: managed by `certbot` (see `/etc/cron.daily/certbot`)
  - Networks:
    - `external_network` - Required for incoming HTTPS reqs
    - `internal_network`

#### Frontend

- **web** (scale: 2)
  - Networks: 
    - `external_network` - Required to connect to other instances
    - `db_network`
    - `es_network`
    - `redis_network`
    - `internal_network` - Alias: `fe_web`
- **streaming** (scale: 2)
  - Networks: 
    - `external_network` - Required to connect to other instances (IS IT????)
    - `db_network`
    - `redis_network`
    - `internal_network` - Alias: `fe_streaming`

#### Backend

- **es** (es_network)
- **redis** (redis_network)
- **db** (db_network)

#### Services

- **sidekiq** (scale: 4)
  - Networks: 
    - `external_network` - Required to connect to other instances
    - `db_network`
    - `es_network`
    - `redis_network`
- **ambassador**
  - Networks: 
    - `external_network` - Required to connect to vulpine.club API
    - `db_network`
- **dbbackup**
  - Networks: 
    - `db_network`

### Content delivery

Currently using Rey's personal AWS account - should probably move to its own...

- S3
- CloudFront

### Backup/DR

- Linode Backup Service
- Hourly rsyncs to Rochester datacenter
