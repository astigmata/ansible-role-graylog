# Changelog

All notable changes to this Ansible role will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2025-07-24

### Added
- Initial release of Graylog Docker stack deployment role
- Support for Graylog 6.3.1 with MongoDB 6.0 and OpenSearch 1.3.16
- Complete container orchestration with health checks
- Automatic system configuration (vm.max_map_count)
- Default GELF UDP input creation
- Template-based Graylog configuration
- Docker network isolation
- Persistent data volumes for all services

### Features
- **Stack Components**:
  - Graylog 6.3.1 server
  - MongoDB 6.0 database
  - OpenSearch 1.3.16 search engine
- **Network Ports**:
  - 9000: Graylog web interface
  - 1514/udp+tcp: Syslog inputs
  - 12201/udp+tcp: GELF inputs
  - 9200: OpenSearch API
  - 27017: MongoDB
- **Data Persistence**: Configurable data directories with proper ownership
- **Security**: Demo credentials with clear production warnings

### Configuration
- Default data directories under `/opt/graylog/`
- OpenSearch compatibility mode for Graylog 6.x
- Basic performance tuning settings
- Automatic password hash generation

### Requirements
- Docker engine
- Ansible collection: `community.docker`
- Minimum 4GB RAM recommended

### Security Notice
⚠️ **This release uses demo credentials and is NOT production-ready**

[0.1.0]: https://github.com/your-org/ansible-role-graylog/releases/tag/v0.1.0