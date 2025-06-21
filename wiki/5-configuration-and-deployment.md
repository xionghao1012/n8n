# Configuration and Deployment | n8n-io/n8n | DeepWiki

This document covers n8n's configuration system and deployment options. It explains how configuration is structured, managed, and applied across different deployment modes including single-instance and distributed scaling scenarios.

For CLI command reference and startup procedures, see [CLI Commands and Configuration](https://deepwiki.com/n8n-io/n8n/5.2-cli-commands-and-configuration). For Docker-specific deployment details, see [Docker Deployment](https://deepwiki.com/n8n-io/n8n/5.1-docker-deployment).

## Configuration Architecture

n8n uses a hierarchical configuration system built around the `GlobalConfig` class, which aggregates multiple specialized configuration modules and supports environment variable overrides.

**Sources:**
- [packages/@n8n/config/src/index.ts](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/src/index.ts)
- [packages/cli/src/config/schema.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/config/schema.ts)

## Deployment Modes

n8n supports two primary execution modes that determine how workflows are processed and scaled.

**Sources:**
- [packages/cli/src/config/schema.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/config/schema.ts)
- [packages/@n8n/config/src/configs/scaling-mode.config.ts](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/src/configs/scaling-mode.config.ts)

## Docker Deployment

n8n provides official Docker images with multi-stage builds optimized for production deployment.

**Sources:**
- [docker/images/n8n/Dockerfile](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/Dockerfile)
- [docker/images/n8n/docker-entrypoint.sh](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/docker-entrypoint.sh)

## Scaling Configuration

n8n's scaling system centers around Redis-backed job queues and worker processes that can be distributed across multiple machines.

**Sources:**
- [packages/cli/src/services/redis-client.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/services/redis-client.service.ts)
- [packages/cli/src/scaling/worker-server.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/worker-server.ts)

## Environment Variable System

n8n uses a comprehensive environment variable system that automatically maps to configuration properties with type validation and file-based secrets support.

**Sources:**
- [packages/@n8n/config/test/config.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/test/config.test.ts)
- [packages/cli/src/services/frontend.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/services/frontend.service.ts)

## Runtime Configuration Management

n8n manages configuration at runtime through the `FrontendService`, which transforms backend configuration into frontend-safe settings and handles dynamic updates.

**Sources:**
- [packages/cli/src/services/frontend.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/services/frontend.service.ts)
- [packages/@n8n/api-types/src/frontend-settings.ts](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/api-types/src/frontend-settings.ts)