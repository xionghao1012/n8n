# 测试框架 | n8n-io/n8n | DeepWiki

本文档介绍n8n全面的测试基础设施，包括使用Cypress进行端到端（E2E）测试、使用Jest进行单元测试、集成测试以及数据库兼容性测试。测试框架确保代码质量、防止回归问题，并在不同环境和数据库引擎中验证功能。

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
* [cypress/constants.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/constants.ts)
* [cypress/e2e/10-undo-redo.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/10-undo-redo.cy.ts)
* [cypress/e2e/11-inline-expression-editor.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/11-inline-expression-editor.cy.ts)
* [cypress/e2e/12-canvas-actions.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/12-canvas-actions.cy.ts)
* [cypress/e2e/12-canvas.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/12-canvas.cy.ts)
* [cypress/e2e/13-pinning.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/13-pinning.cy.ts)
* [cypress/e2e/14-data-transformation-expressions.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/14-data-transformation-expressions.cy.ts)
* [cypress/e2e/14-mapping.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/14-mapping.cy.ts)
* [cypress/e2e/15-scheduler-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/15-scheduler-node.cy.ts)
* [cypress/e2e/16-webhook-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/16-webhook-node.cy.ts)
* [cypress/e2e/41-editors.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/41-editors.cy.ts)
* [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
* [cypress/e2e/6-code-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/6-code-node.cy.ts)
* [cypress/e2e/7-workflow-actions.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/7-workflow-actions.cy.ts)
* [cypress/e2e/8-http-request-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/8-http-request-node.cy.ts)
* [cypress/e2e/9-expression-editor-modal.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/9-expression-editor-modal.cy.ts)
* [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
* [cypress/pages/workflow.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/workflow.ts)
* [cypress/support/commands.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/support/commands.ts)
* [cypress/support/e2e.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/support/e2e.ts)
* [cypress/support/index.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/support/index.ts)

## 测试策略概述

n8n采用多层测试方法，包括端到端测试、单元测试、集成测试和数据库兼容性测试。测试框架基于现代工具构建，并遵循行业最佳实践以确保可维护性和可靠性。

### 测试类型与覆盖范围

| 测试类型 | 框架 | 目的 | 位置 |
| --- | --- | --- | --- |
| E2E测试 | Cypress | 用户工作流验证 | `cypress/e2e/` |
| 单元测试 | Jest | 组件/函数测试 | 各种`*.test.ts`文件 |
| 集成测试 | Jest | API和服务测试 | `packages/cli/test/integration/` |
| 数据库测试 | Jest | 多数据库兼容性 | 数据库特定测试套件 |

## Cypress端到端测试框架

端到端测试框架使用Cypress模拟真实用户交互并验证完整工作流。测试采用页面对象（Page Object）模式组织，以提高可维护性和可重用性。

### 核心页面对象

测试框架通过几个关键类实现页面对象模式：

* **NDV（节点详情视图）**：提供全面的节点交互测试工具
* **WorkflowPage**：处理画布级操作和工作流管理

### 关键测试组件

`NDV`类提供：

* **参数输入测试**：表单验证方法
* **执行测试**：工作流执行验证
* **数据验证**：数据流测试
* **表达式测试**：表达式验证

`WorkflowPage`类处理：

* **节点管理**：添加、删除、复制节点
* **工作流操作**：保存、执行、激活工作流
* **画布交互**：缩放、选择、拖放操作

### 测试执行与支持

支持系统提供必要的测试工具：

* **认证命令**：基于角色的测试
* **工作流管理**：从JSON fixtures加载测试工作流
* **自定义交互**：复杂UI交互
* **数据库重置**：测试之间的干净状态

## CI/CD测试流水线

测试流水线通过GitHub Actions工作流实现，根据触发器和条件运行不同的测试套件。

### 测试并行化与分布

端到端测试框架支持跨多个容器的并行执行：

* **容器矩阵**：测试可在多达15个并行容器上运行
* **测试规范分布**：各个测试规范分布在不同容器上
* **Cypress仪表板**：测试记录和并行协调集成
* **唯一构建ID**：每个测试运行获取唯一标识符

## 数据库兼容性测试

n8n支持多种数据库引擎，测试框架验证所有支持数据库的兼容性。

### 数据库测试矩阵

每个数据库引擎都有特定的测试配置：

* **SQLite Pooled**：测试连接池
* **PostgreSQL**：使用最小池大小测试以检测死锁
* **MySQL变体**：测试多个MySQL版本的兼容性
* **MariaDB**：验证MariaDB特定行为和兼容性

数据库测试使用延长的超时时间，以适应较慢的数据库操作和容器启动时间。

## 单元测试与集成测试

单元测试框架使用Jest，通过全面的测试套件覆盖前端和后端组件。

### 测试执行与覆盖率

单元测试系统提供：

* **后端测试**：运行所有后端相关测试
* **节点测试**：执行节点特定测试套件
* **前端测试**：验证UI组件和交互
* **覆盖率收集**：可配置的覆盖率跟踪
* **Codecov集成**：自动上传测试结果和覆盖率数据

测试框架支持多个Node.js版本，其中22.x版本是覆盖率收集的主要版本。

## 测试数据与Fixtures

测试框架使用全面的fixture系统提供一致的测试数据和工作流定义。

### Fixture组织

测试fixtures按功能组织，提供真实的测试场景：

* **工作流Fixtures**：包含完整工作流定义的JSON文件
* **节点配置**：预配置的节点设置
* **测试数据**：样本输入/输出数据
* **二进制测试文件**：支持测试文件上传和二进制数据处理

`createFixtureWorkflow()`命令从fixtures目录加载工作流，并自动设置测试环境。

### 测试环境管理

测试环境管理确保：

* **干净状态**：每个测试都以全新的数据库状态开始
* **正确认证**：基于角色的认证
* **网络处理**：API调用和加载状态的一致处理
* **错误处理**：控制台错误和未捕获异常的优雅处理