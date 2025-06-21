# 节点系统

节点系统是n8n用于与外部服务集成和执行数据转换的可扩展架构。本文档涵盖核心节点实现框架、内置节点目录、凭据管理、版本控制系统和扩展生态系统。

## 节点架构概述

n8n节点系统围绕`INodeType`接口构建，该接口定义了所有可执行节点的契约。节点被组织成包，核心`n8n-nodes-base`包包含400多个内置集成。

### 关键组件

- **核心节点框架**：`INodeType`接口
- **节点包**：`n8n-nodes-base`（400+节点）、`@n8n/nodes-langchain`（AI/ML节点）
- **开发工具**：`n8n-node-dev` CLI

## 节点实现结构

每个节点都实现`INodeType`接口，包含：

- `description`：节点元数据和UI定义
- `execute()`：主要执行逻辑
- `properties`：配置参数
- `credentials`：身份验证要求

## 内置节点类别

| 类别 | 示例 | 用途 |
|----------|----------|---------|
| 通信 | Slack、Email | 消息传递 |
| 云存储 | Google Drive、S3 | 文件管理 |
| 数据库 | PostgreSQL、MongoDB | 数据持久化 |
| AI/ML | OpenAI、LangChain | AI服务 |
| 实用工具 | HTTP Request、Code | 通用操作 |

## 节点版本控制系统

n8n使用`VersionedNodeType`管理节点的多个版本，同时保持向后兼容性。

## 凭据集成

节点通过标准化接口（`ICredentialType`）与凭据系统集成。凭据可在多个节点间共享。

## 开发工作流

`n8n-node-dev`包提供CLI工具用于：

- 创建新节点
- 生成凭据类型
- 测试节点实现

## AI/ML节点生态系统

`@n8n/nodes-langchain`包为n8n扩展了AI功能，包括：

- 语言模型
- 向量存储
- 文档处理
- AI代理和链