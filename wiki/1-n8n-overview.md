n8n Overview
------------

Relevant source files
*   [CHANGELOG.md](https://github.com/xionghao1012/n8n/blob/master/CHANGELOG.md)
*   [README.md](https://github.com/xionghao1012/n8n/blob/master/README.md)
*   [docker/images/n8n/README.md](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/README.md)
*   [package.json](https://github.com/xionghao1012/n8n/blob/master/package.json)
*   [packages/@n8n/config/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/package.json)
*   [packages/@n8n/nodes-langchain/README.md](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/README.md)
*   [packages/@n8n/nodes-langchain/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json)
*   [packages/cli/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json)
*   [packages/core/README.md](https://github.com/xionghao1012/n8n/blob/master/packages/core/README.md)
*   [packages/core/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/core/package.json)
*   [packages/node-dev/README.md](https://github.com/xionghao1012/n8n/blob/master/packages/node-dev/README.md)
*   [packages/node-dev/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/node-dev/package.json)
*   [packages/nodes-base/README.md](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/README.md)
*   [packages/nodes-base/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json)
*   [packages/workflow/README.md](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/README.md)
*   [packages/workflow/package.json](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/package.json)
*   [pnpm-lock.yaml](https://github.com/xionghao1012/n8n/blob/master/pnpm-lock.yaml)
*   [pnpm-workspace.yaml](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml)

This document provides a comprehensive overview of the n8n workflow automation platform architecture, covering the core system components, execution models, and extensibility mechanisms. It serves as an entry point for understanding how the various packages and modules work together to enable workflow automation.

For detailed information about specific subsystems, see [Core Packages](https://deepwiki.com/n8n-io/n8n/1.1-core-packages), [Workflow Execution Engine](https://deepwiki.com/n8n-io/n8n/2-workflow-execution-engine), [Node System](https://deepwiki.com/n8n-io/n8n/3-node-system), [User Interface](https://deepwiki.com/n8n-io/n8n/4-user-interface), and [Configuration and Deployment](https://deepwiki.com/n8n-io/n8n/5-configuration-and-deployment).

Platform Architecture
---------------------

n8n is built as a TypeScript monorepo containing multiple interconnected packages that provide workflow automation capabilities. The platform consists of a core execution engine, an extensible node system, a web-based editor, and deployment infrastructure.

### Core System Components

**Sources:**[packages/cli/package.json 1-186](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L1-L186)[packages/core/package.json 1-77](https://github.com/xionghao1012/n8n/blob/master/packages/core/package.json#L1-L77)[packages/workflow/package.json 1-61](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/package.json#L1-L61)[packages/nodes-base/package.json 1-2000](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json#L1-L2000)[packages/@n8n/nodes-langchain/package.json 1-220](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json#L1-L220)[packages/@n8n/config/package.json 1-31](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/package.json#L1-L31)

### Execution Architecture

The platform supports two primary execution modes with different scaling characteristics:

**Sources:**[packages/cli/package.json 24-36](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L24-L36)[package.json 36-46](https://github.com/xionghao1012/n8n/blob/master/package.json#L36-L46)

Package Dependencies and Module Structure
-----------------------------------------

The monorepo is organized with clear dependency relationships and module boundaries:

### Dependency Hierarchy

| Package | Purpose | Key Dependencies |
| --- | --- | --- |
| `n8n` (CLI) | Main application entry point | n8n-core, n8n-workflow, n8n-nodes-base, n8n-editor-ui |
| `n8n-core` | Core execution functionality | n8n-workflow, @n8n/config |
| `n8n-workflow` | Workflow definition and utilities | Base TypeScript types |
| `n8n-nodes-base` | Built-in node integrations | n8n-workflow |
| `n8n-editor-ui` | Web interface | Vue.js, Element Plus |
| `@n8n/nodes-langchain` | AI/LangChain nodes | langchain, n8n-workflow |
| `@n8n/config` | Configuration management | Zod validation |

**Sources:**[packages/cli/package.json 88-185](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L88-L185)[packages/core/package.json 39-76](https://github.com/xionghao1012/n8n/blob/master/packages/core/package.json#L39-L76)[packages/workflow/package.json 43-60](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/package.json#L43-L60)[packages/nodes-base/package.json 1-2000](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json#L1-L2000)

### Node Registration System

**Sources:**[packages/nodes-base/package.json 23-410](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json#L23-L410)[packages/@n8n/nodes-langchain/package.json 23-140](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json#L23-L140)

Technology Stack and Build System
---------------------------------

The platform uses modern JavaScript/TypeScript tooling for development and build processes:

### Build and Development Tools

| Tool | Purpose | Configuration |
| --- | --- | --- |
| `pnpm` | Package manager | [pnpm-workspace.yaml 1-70](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml#L1-L70) |
| `turbo` | Monorepo build orchestration | [package.json 10-47](https://github.com/xionghao1012/n8n/blob/master/package.json#L10-L47) |
| `TypeScript` | Type checking and compilation | `tsconfig.build.json` files |
| `tsup` | Fast TypeScript bundler | Node packages |
| `Vite` | Frontend development and building | Editor UI |
| `Jest` | Testing framework | Unit and integration tests |
| `Cypress` | End-to-end testing | [cypress/](https://github.com/xionghao1012/n8n/blob/master/cypress/) directory |

**Sources:**[package.json 2-112](https://github.com/xionghao1012/n8n/blob/master/package.json#L2-L112)[pnpm-workspace.yaml 1-70](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml#L1-L70)[pnpm-lock.yaml 1-2000](https://github.com/xionghao1012/n8n/blob/master/pnpm-lock.yaml#L1-L2000)

### Runtime Dependencies

The platform leverages several key runtime libraries:

**Sources:**[packages/cli/package.json 88-185](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L88-L185)[packages/@n8n/nodes-langchain/package.json 154-219](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json#L154-L219)[pnpm-workspace.yaml 8-70](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml#L8-L70)

Deployment and Configuration
----------------------------

n8n supports multiple deployment strategies with comprehensive configuration options:

### Deployment Options

| Method | Entry Point | Use Case |
| --- | --- | --- |
| npm/npx | `npx n8n` | Development and testing |
| Docker | `docker.n8n.io/n8nio/n8n` | Production deployment |
| Docker Compose | Multiple services | Complex deployments |
| Self-hosted | Binary installation | Custom environments |
| n8n Cloud | Hosted service | Managed deployment |

**Sources:**[README.md 17-32](https://github.com/xionghao1012/n8n/blob/master/README.md#L17-L32)[docker/images/n8n/README.md 56-95](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/README.md#L56-L95)

### Configuration Management

The configuration system uses environment variables and file-based configuration:

**Sources:**[docker/images/n8n/README.md 97-138](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/README.md#L97-L138)[packages/@n8n/config/package.json 1-31](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/package.json#L1-L31)

This architecture provides a flexible foundation for workflow automation that scales from single-user development scenarios to enterprise-grade deployments with distributed execution and AI capabilities.