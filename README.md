![Banner image](https://user-images.githubusercontent.com/10284570/173569848-c624317f-42b1-45a6-ab09-f0ea3c247648.png)

# n8n - 面向技术团队的安全工作流自动化平台

n8n 是一款工作流自动化平台，为技术团队提供代码级灵活性与无代码级速度。凭借 400+ 集成、原生 AI 能力和公平代码许可，n8n 让您在构建强大自动化流程的同时，完全掌控数据与部署。



## 核心能力

- **按需编码**: 使用 JavaScript/Python 编写逻辑、添加 npm 包或可视化操作
- **原生 AI 平台**: 基于 LangChain 构建 AI 智能体工作流，使用自有数据和模型
- **完全掌控**: 通过公平代码许可自托管，或使用 [云端服务](https://app.n8n.cloud/login)
- **企业级支持**: 高级权限管理、单点登录 (SSO) 和物理隔离部署
- **活跃社区**: 400+ 集成与 900+ 开箱即用 [模板](https://n8n.io/workflows)

## 快速开始

通过 [npx](https://docs.n8n.io/hosting/installation/npm/)立即体验 (需安装 [Node.js](https://nodejs.org/en/)):

```
npx n8n
```

或使用 [Docker](https://docs.n8n.io/hosting/installation/docker/)部署:

```
docker volume create n8n_data
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

访问编辑器 http://localhost:5678

## 资源导航

- 📚 [官方文档](https://docs.n8n.io)
- 🔧 [400+ 集成列表](https://n8n.io/integrations)
- 💡 [工作流示例](https://n8n.io/workflows)
- 🤖 [AI & LangChain 指南](https://docs.n8n.io/langchain/)
- 👥 [社区论坛](https://community.n8n.io)
- 📖 [社区教程](https://community.n8n.io/c/tutorials/28)

## 技术支持

需要帮助？社区论坛是获取支持的最佳渠道:
[community.n8n.io](https://community.n8n.io)

## 许可协议

n8n is [fair-code](https://faircode.io) distributed under the [Sustainable Use License](https://github.com/n8n-io/n8n/blob/master/LICENSE.md) and [n8n Enterprise License](https://github.com/n8n-io/n8n/blob/master/LICENSE_EE.md).

- **Source Available**: Always visible source code
- **Self-Hostable**: Deploy anywhere
- **Extensible**: Add your own nodes and functionality

[Enterprise licenses](mailto:license@n8n.io) available for additional features and support.

Additional information about the license model can be found in the [docs](https://docs.n8n.io/reference/license/).

## 共享指南

Found a bug 🐛 or have a feature idea ✨? Check our [Contributing Guide](https://github.com/n8n-io/n8n/blob/master/CONTRIBUTING.md) to get started.

## 加入团队

愿与我们共同塑造自动化未来？查看 [职位列表](https://n8n.io/careers) 加入团队!

## n8n 名称含义?

**简答:** 意为 "nodemation"（节点自动化），发音为 /n-eɪt-n/（n-eight-n）。

**详答:** "我经常被问到这个问题（比预期频繁得多），因此决定在此说明。在为项目寻找可用域名时，我发现所有理想的名称均被占用。最终我选择了 'nodemation'——'node' 既代表节点视图（Node-View），也指代 Node.js 技术；'-mation' 则取自 'automation'（自动化），体现项目核心价值。但名称过长不利于 CLI 操作，故简化为 'n8n'。" - **Jan Oberhauser, n8n.io 创始人兼 CEO**
