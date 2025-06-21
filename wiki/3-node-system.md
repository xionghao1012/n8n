# Node System

The Node System is n8n's extensible architecture for integrating with external services and performing data transformations. This document covers the core node implementation framework, built-in node catalog, credential management, versioning system, and the extension ecosystem.

## Node Architecture Overview

The n8n node system is built around the `INodeType` interface, which defines the contract for all executable nodes. Nodes are organized into packages, with the core `n8n-nodes-base` package containing over 400 built-in integrations.

### Key Components

- **Core Node Framework**: `INodeType` interface
- **Node Packages**: `n8n-nodes-base` (400+ nodes), `@n8n/nodes-langchain` (AI/ML nodes)
- **Development Tools**: `n8n-node-dev` CLI

## Node Implementation Structure

Every node implements the `INodeType` interface with:

- `description`: Node metadata and UI definition
- `execute()`: Main execution logic
- `properties`: Configuration parameters
- `credentials`: Authentication requirements

## Built-in Node Categories

| Category | Examples | Purpose |
|----------|----------|---------|
| Communication | Slack, Email | Messaging |
| Cloud Storage | Google Drive, S3 | File management |
| Databases | PostgreSQL, MongoDB | Data persistence |
| AI/ML | OpenAI, LangChain | AI services |
| Utilities | HTTP Request, Code | General operations |

## Node Versioning System

n8n uses `VersionedNodeType` to manage multiple versions of nodes while maintaining backward compatibility.

## Credential Integration

Nodes integrate with the credential system through standardized interfaces (`ICredentialType`). Credentials can be shared across multiple nodes.

## Development Workflow

The `n8n-node-dev` package provides CLI tools for:

- Creating new nodes
- Generating credential types
- Testing node implementations

## AI/ML Node Ecosystem

The `@n8n/nodes-langchain` package extends n8n with AI capabilities including:

- Language models
- Vector stores
- Document processing
- AI agents and chains