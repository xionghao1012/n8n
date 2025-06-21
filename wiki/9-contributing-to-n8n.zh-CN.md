# 为n8n做贡献 | n8n-io/n8n | DeepWiki

本文档介绍了n8n项目的开发工作流、CI/CD流程和贡献指南。它解释了从初始开发到生产部署过程中管理代码质量、测试和发布的自动化系统。

## 相关源文件

* [.github/scripts/bump-versions.mjs](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/bump-versions.mjs)
* [.github/scripts/package.json](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/package.json)
* [.github/scripts/update-changelog.mjs](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/update-changelog.mjs)
* [.github/workflows/check-documentation-urls.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-documentation-urls.yml)
* [.github/workflows/check-pr-title.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-pr-title.yml)
* [.github/workflows/check-run-eligibility.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-run-eligibility.yml)
* [.github/workflows/chromatic.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/chromatic.yml)
* [.github/workflows/ci-master.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-master.yml)
* [.github/workflows/ci-postgres-mysql.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-postgres-mysql.yml)
* [.github/workflows/ci-pull-requests.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-pull-requests.yml)
* [.github/workflows/docker-base-image.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/docker-base-image.yml)
* [.github/workflows/docker-images-nightly.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/docker-images-nightly.yml)
* [.github/workflows/e2e-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-reusable.yml)
* [.github/workflows/e2e-tests-pr.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-tests-pr.yml)
* [.github/workflows/e2e-tests.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-tests.yml)
* [.github/workflows/linting-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/linting-reusable.yml)
* [.github/workflows/release-create-pr.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-create-pr.yml)
* [.github/workflows/release-publish.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-publish.yml)
* [.github/workflows/release-push-to-channel.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-push-to-channel.yml)
* [.github/workflows/security-trivy-scan-callable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/security-trivy-scan-callable.yml)
* [.github/workflows/test-workflows-nightly.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-nightly.yml)
* [.github/workflows/test-workflows-pr-approved.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-pr-approved.yml)
* [.github/workflows/test-workflows-pr-comment.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-pr-comment.yml)
* [.github/workflows/units-tests-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/units-tests-reusable.yml)
* [CONTRIBUTING.md](https://github.com/xionghao1012/n8n/blob/master/CONTRIBUTING.md)

## 开发工作流

n8n项目采用以单体仓库管理、自动化测试和严格质量关卡为中心的结构化开发工作流。

### 开发环境设置

开发设置遵循使用`pnpm`工作区的标准单体仓库模式：

| 组件 | 工具/技术 | 配置文件 |
| --- | --- | --- |
| 包管理器 | 带corepack的pnpm | `.packageManagerrc` |
| Node.js版本 | 22.x | 多个工作流文件 |
| 构建系统 | Turbo | `turbo.json` |
| 代码检查 | ESLint/Prettier | 多个配置文件 |
| 测试 | Jest、Cypress | 测试配置文件 |

项目对社区贡献有严格要求。

## CI/CD管道架构

n8n CI/CD系统使用GitHub Actions和多个相互关联的工作流，以实现全面的质量保证和自动化部署。

### 核心CI工作流

主要CI管道包括：
- 拉取请求验证
- 主分支测试
- 数据库兼容性测试
- 端到端测试

### 数据库测试矩阵

项目通过专用测试工作流保持跨多个数据库引擎的兼容性。

### E2E测试系统

端到端测试使用Cypress，支持并行执行和基于审批的触发。

## 测试框架架构

测试系统包含多层和多种类型的测试，并提供全面的覆盖率报告。

### 测试执行矩阵

全面的测试管道包括：
- 单元测试
- 集成测试
- 数据库测试
- 端到端测试

### 测试资格和审批系统

项目使用资格系统确定何时应运行全面测试。

## 发布管理系统

发布系统通过GitHub Actions工作流自动执行版本更新、变更日志生成和多渠道发布。

### 发布创建管道

自动化发布过程包括：
- 版本更新
- 变更日志生成
- 发布PR创建

### 发布发布管道

多渠道发布分发系统处理：
- Docker镜像发布
- NPM包发布
- GitHub发布创建

### 渠道管理系统

项目支持多个发布渠道，并具有自动标记功能。

## 代码质量和安全

项目通过集成到CI/CD管道中的自动化检查和安全扫描来保持高代码质量。

### 质量关卡系统

代码质量强制管道包括：
- 代码检查
- 类型检查
- 测试覆盖率要求

### 安全扫描集成

安全漏洞检测系统包括：
- 依赖项扫描
- 容器扫描
- 代码扫描

## 基础设施和部署

项目使用基于Docker的部署，支持多架构和自动化夜间构建。

### Docker构建系统

容器构建和分发管道处理：
- 多架构构建
- 夜间构建
- 发布构建

此贡献系统通过自动化CI/CD管道确保代码质量、全面测试和可靠的发布管理，这些管道可从个人贡献扩展到跨多个分发渠道的生产部署。