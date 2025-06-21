# n8n 概述

相关源文件
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

本文档全面概述了n8n工作流自动化平台的架构，涵盖核心系统组件、执行模型和扩展机制。它是理解各个包和模块如何协同工作以实现工作流自动化的入口。

有关特定子系统的详细信息，请参阅[核心包](https://deepwiki.com/n8n-io/n8n/1.1-core-packages)、[工作流执行引擎](https://deepwiki.com/n8n-io/n8n/2-workflow-execution-engine)、[节点系统](https://deepwiki.com/n8n-io/n8n/3-node-system)、[用户界面](https://deepwiki.com/n8n-io/n8n/4-user-interface)和[配置与部署](https://deepwiki.com/n8n-io/n8n/5-configuration-and-deployment)。

平台架构
---------------------

n8n构建为一个TypeScript monorepo，包含多个相互连接的包，提供工作流自动化功能。该平台由核心执行引擎、可扩展的节点系统、基于Web的编辑器和部署基础设施组成。

### 核心系统组件

**来源:**[packages/cli/package.json 1-186](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L1-L186)[packages/core/package.json 1-77](https://github.com/xionghao1012/n8n/blob/master/packages/core/package.json#L1-L77)[packages/workflow/package.json 1-61](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/package.json#L1-L61)[packages/nodes-base/package.json 1-2000](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json#L1-L2000)[packages/@n8n/nodes-langchain/package.json 1-220](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json#L1-L220)[packages/@n8n/config/package.json 1-31](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/package.json#L1-L31)

### 执行架构

平台支持两种主要执行模式，具有不同的扩展特性：

**来源:**[packages/cli/package.json 24-36](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L24-L36)[package.json 36-46](https://github.com/xionghao1012/n8n/blob/master/package.json#L36-L46)

包依赖关系和模块结构
-----------------------------------------

monorepo通过清晰的依赖关系和模块边界进行组织：

### 依赖层次结构

| 包 | 用途 | 关键依赖 |
| --- | --- | --- |
| `n8n` (CLI) | 主应用程序入口点 | n8n-core, n8n-workflow, n8n-nodes-base, n8n-editor-ui |
| `n8n-core` | 核心执行功能 | n8n-workflow, @n8n/config |
| `n8n-workflow` | 工作流定义和实用工具 | 基础TypeScript类型 |
| `n8n-nodes-base` | 内置节点集成 | n8n-workflow |
| `n8n-editor-ui` | Web界面 | Vue.js, Element Plus |
| `@n8n/nodes-langchain` | AI/LangChain节点 | langchain, n8n-workflow |
| `@n8n/config` | 配置管理 | Zod验证 |

**来源:**[packages/cli/package.json 88-185](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L88-L185)[packages/core/package.json 39-76](https://github.com/xionghao1012/n8n/blob/master/packages/core/package.json#L39-L76)[packages/workflow/package.json 43-60](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/package.json#L43-L60)[packages/nodes-base/package.json 1-2000](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json#L1-L2000)

### 节点注册系统

**来源:**[packages/nodes-base/package.json 23-410](https://github.com/xionghao1012/n8n/blob/master/packages/nodes-base/package.json#L23-L410)[packages/@n8n/nodes-langchain/package.json 23-140](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json#L23-L140)

技术栈和构建系统
---------------------------------

平台使用现代JavaScript/TypeScript工具进行开发和构建过程：

### 构建和开发工具

| 工具 | 用途 | 配置 |
| --- | --- | --- |
| `pnpm` | 包管理器 | [pnpm-workspace.yaml 1-70](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml#L1-L70) |
| `turbo` | Monorepo构建编排 | [package.json 10-47](https://github.com/xionghao1012/n8n/blob/master/package.json#L10-L47) |
| `TypeScript` | 类型检查和编译 | `tsconfig.build.json` 文件 |
| `tsup` | 快速TypeScript打包工具 | Node包 |
| `Vite` | 前端开发和构建 | 编辑器UI |
| `Jest` | 测试框架 | 单元和集成测试 |
| `Cypress` | 端到端测试 | [cypress/](https://github.com/xionghao1012/n8n/blob/master/cypress/) 目录 |

**来源:**[package.json 2-112](https://github.com/xionghao1012/n8n/blob/master/package.json#L2-L112)[pnpm-workspace.yaml 1-70](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml#L1-L70)[pnpm-lock.yaml 1-2000](https://github.com/xionghao1012/n8n/blob/master/pnpm-lock.yaml#L1-L2000)

### 运行时依赖

平台利用了几个关键的运行时库：

**来源:**[packages/cli/package.json 88-185](https://github.com/xionghao1012/n8n/blob/master/packages/cli/package.json#L88-L185)[packages/@n8n/nodes-langchain/package.json 154-219](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/nodes-langchain/package.json#L154-L219)[pnpm-workspace.yaml 8-70](https://github.com/xionghao1012/n8n/blob/master/pnpm-workspace.yaml#L8-L70)

部署和配置
----------------------------

n8n支持多种部署策略和全面的配置选项：

### 部署选项

| 方法 | 入口点 | 使用场景 |
| --- | --- | --- |
| npm/npx | `npx n8n` | 开发和测试 |
| Docker | `docker.n8n.io/n8nio/n8n` | 生产部署 |
| Docker Compose | 多个服务 | 复杂部署 |
| 自托管 | 二进制安装 | 自定义环境 |
| n8n Cloud | 托管服务 | 托管部署 |

**来源:**[README.md 17-32](https://github.com/xionghao1012/n8n/blob/master/README.md#L17-L32)[docker/images/n8n/README.md 56-95](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/README.md#L56-L95)

### 配置管理

配置系统使用环境变量和基于文件的配置：

**来源:**[docker/images/n8n/README.md 97-138](https://github.com/xionghao1012/n8n/blob/master/docker/images/n8n/README.md#L97-L138)[packages/@n8n/config/package.json 1-31](https://github.com/xionghao1012/n8n/blob/master/packages/@n8n/config/package.json#L1-L31)

该架构为工作流自动化提供了灵活的基础，可从单用户开发场景扩展到具有分布式执行和AI功能的企业级部署。