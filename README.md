# Graylog Docker Stack

Ansible role to deploy a complete Graylog stack with MongoDB and OpenSearch using Docker containers.

## Stack Components

- **Graylog 6.3.1** - Log management platform
- **MongoDB 6.0** - Database backend  
- **OpenSearch 1.3.16** - Search engine

## Requirements

- Docker and docker-compose installed
- Ansible collection: `community.docker`
- Target system with sufficient resources (4GB+ RAM recommended)

## Quick Start

```yaml
- hosts: graylog_servers
  become: yes
  roles:
    - astigmata.ansible-role-graylog
```

## Default Configuration

### Access
- **Web Interface**: http://localhost:9000
- **Username**: admin
- **Password**: admin

### Ports
- 9000: Graylog web interface
- 1514/udp+tcp: Syslog
- 12201/udp+tcp: GELF
- 9200: OpenSearch
- 27017: MongoDB

### Data Directories
- `/opt/graylog/data` - Graylog data
- `/opt/graylog/mongodb` - MongoDB data
- `/opt/graylog/opensearch` - OpenSearch data

## Key Variables

```yaml
# Versions
graylog_version: "6.3.1"
opensearch_version: "1.3.16"
mongodb_version: "6.0"

# Credentials (CHANGE IN PRODUCTION)
graylog_admin_password: "admin"
mongodb_root_password: "mongopass123"
opensearch_admin_password: "OpenSearch123!"

# Data directories
graylog_data_dir: "/opt/graylog/data"
mongodb_data_dir: "/opt/graylog/mongodb"
opensearch_data_dir: "/opt/graylog/opensearch"
```

## Production Deployment

1. Override default credentials:
```yaml
vars:
  graylog_admin_password: "{{ vault_graylog_password }}"
  mongodb_root_password: "{{ vault_mongodb_password }}"
  opensearch_admin_password: "{{ vault_opensearch_password }}"
```

2. Use Ansible Vault for sensitive data
3. Adjust memory settings in OpenSearch configuration
4. Configure firewall rules appropriately

## Compatibility Notes

- OpenSearch 1.3.16 used for Graylog 6.x compatibility
- `compatibility.override_main_response_version: true` enables Elasticsearch API compatibility
- Security plugins disabled for simplified setup

## Troubleshooting

### Container Health Checks
All containers have built-in health checks. Check status:
```bash
docker ps
docker logs graylog_server
```

### Common Issues
- **vm.max_map_count**: Automatically set to 262144 for OpenSearch
- **Permissions**: Data directories owned by correct UIDs (1000/1100)
- **Network**: All containers use `graylog_network` bridge

## Security Warning

⚠️ **This configuration uses demo credentials and is NOT production-ready**

Change all default passwords and review security settings before production use.
