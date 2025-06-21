# 用户界面 | n8n-io/n8n | DeepWiki

本文档介绍了提供n8n工作流编辑器界面的Vue.js前端应用程序。UI系统包括主工作流画布、节点配置视图、数据可视化组件、参数输入系统和全面的状态管理。

有关驱动后端的工作流执行引擎的信息，请参见[工作流执行引擎](https://deepwiki.com/n8n-io/n8n/2-workflow-execution-engine)。有关节点系统和集成的详细信息，请参见[节点系统](https://deepwiki.com/n8n-io/n8n/3-node-system)。

## 前端架构

n8n用户界面是作为Vue.js 3单页应用程序构建的，使用Composition API、TypeScript和Pinia进行状态管理。该应用程序被构造为位于`packages/frontend/editor-ui/`中的monorepo包。

### 核心UI架构

来源：
- [packages/frontend/editor-ui/src/views/NodeView.vue](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/views/NodeView.vue)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)

## 节点详情视图（NDV）

节点详情视图是配置各个工作流节点的主要界面。它在滑动面板界面中提供参数输入、数据可视化和执行控制。

### NDV组件结构

### NDV操作和交互

NDV通过类型化操作支持全面的节点配置：

| 操作类别 | NDV方法 | 用途 |
| --- | --- | --- |
| 执行 | `NDV.actions.execute()`、`NDV.actions.executePrevious()` | 测试节点执行 |
| 数据管理 | `NDV.actions.pinData()`、`NDV.actions.setPinnedData()` | 固定执行结果 |
| 参数输入 | `NDV.actions.typeIntoParameterInput()`、`NDV.actions.clearParameterInput()` | 配置节点参数 |
| 视图切换 | `NDV.actions.switchInputMode()`、`NDV.actions.switchOutputMode()` | 更改数据显示格式 |
| 表达式编辑 | `NDV.actions.openInlineExpressionEditor()`、`NDV.actions.validateExpressionPreview()` | 编辑表达式 |

来源：
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)

## 参数输入系统

参数输入系统处理节点配置的动态表单生成，支持各种输入类型和验证模式。

### 参数输入组件

来源：
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)

## 状态管理系统

该应用程序使用Pinia存储来管理组件间的全局状态。每个存储遵循Composition API模式并处理特定的领域区域。

### 核心存储架构

### 设置存储配置

`useSettingsStore`管理前端配置和企业功能标志：

| 配置区域 | 存储属性 | API来源 |
| --- | --- | --- |
| 企业功能 | `isEnterpriseFeatureEnabled` | `/rest/settings`端点 |
| 部署类型 | `deploymentType`、`isCloudDeployment` | `FrontendSettings.deployment` |
| 认证 | `isLdapLoginEnabled`、`isSamlLoginEnabled` | `FrontendSettings.sso` |
| AI功能 | `isAiAssistantEnabled`、`isAskAiEnabled` | `FrontendSettings.aiAssistant` |
| 模板 | `isTemplatesEnabled`、`templatesHost` | `FrontendSettings.templates` |

来源：
- [packages/frontend/editor-ui/src/stores/settings.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/settings.store.ts)
- [packages/frontend/editor-ui/src/stores/users.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/users.store.ts)
- [packages/frontend/editor-ui/src/stores/ui.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/ui.store.ts)

## 数据可视化组件

UI提供多种视图用于显示和交互工作流执行数据，支持不同的可视化模式和数据探索模式。

### 运行数据显示模式

### 数据搜索和过滤

数据可视化系统支持全面的搜索和过滤功能：

| 功能 | 实现 | 测试覆盖 |
| --- | --- | --- |
| 文本搜索 | `ndv-search`组件 | 跨JSON/表格数据搜索 |
| 模式搜索 | 模式字段过滤 | 预输入字段搜索 |
| 数据高亮 | Mark.js集成 | 搜索词高亮显示 |
| 分页 | `ndv-data-pagination` | 大型数据集处理 |
| 项目计数显示 | `ndv-items-count` | 结果计数指示器 |

来源：
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)

## 模态框和对话框系统

UI实现了一个集中式模态框系统，用于管理整个应用程序中的对话框和覆盖层。

### 模态框系统架构

系统将超过35种不同的模态框类型定义为常量，支持应用程序中类型安全的模态框管理。

来源：
- [packages/frontend/editor-ui/src/constants.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/constants.ts)
- [packages/frontend/editor-ui/src/stores/ui.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/ui.store.ts)
- [packages/frontend/editor-ui/src/Interface.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/Interface.ts)

## 工作流画布和编辑器

主工作流编辑器提供了一个可视化画布，用于通过拖放功能和实时执行反馈构建和编辑工作流。

### 画布组件架构

### 画布交互模式

工作流画布支持全面的工作流构建交互模式：

| 交互类型 | 实现 | 测试覆盖 |
| --- | --- | --- |
| 节点添加 | `WorkflowPage.actions.addNodeToCanvas()` | 通过加号按钮或节点创建器添加节点 |
| 节点删除 | 上下文菜单+键盘快捷键 | 删除单个或多个节点 |
| 节点移动 | 带位置跟踪的拖放 | 实时位置更新 |
| 连接管理 | 端点间拖动 | 创建、删除和修改连接 |
| 画布导航 | 缩放、平移、适合屏幕 | 视口变换控制 |
| 节点执行 | 上下文菜单执行 | 测试单个节点 |

来源：
- [packages/frontend/editor-ui/src/views/NodeView.vue](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/views/NodeView.vue)
- [cypress/pages/workflow.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/workflow.ts)
- [cypress/e2e/12-canvas.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/12-canvas.cy.ts)

## 表达式编辑器系统

表达式编辑器为节点参数内的动态表达式和代码编辑提供复杂支持。

### 表达式编辑器组件

来源：
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
- [cypress/e2e/11-inline-expression-editor.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/11-inline-expression-editor.cy.ts)