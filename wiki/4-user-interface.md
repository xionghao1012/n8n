# User Interface | n8n-io/n8n | DeepWiki

This document describes the Vue.js frontend application that provides n8n's workflow editor interface. The UI system encompasses the main workflow canvas, node configuration views, data visualization components, parameter input systems, and comprehensive state management.

For information about the workflow execution engine that powers the backend, see [Workflow Execution Engine](https://deepwiki.com/n8n-io/n8n/2-workflow-execution-engine). For details about the node system and integrations, see [Node System](https://deepwiki.com/n8n-io/n8n/3-node-system).

## Frontend Architecture

The n8n user interface is built as a Vue.js 3 single-page application using the Composition API, TypeScript, and Pinia for state management. The application is structured as a monorepo package located in `packages/frontend/editor-ui/`.

### Core UI Architecture

Sources:
- [packages/frontend/editor-ui/src/views/NodeView.vue](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/views/NodeView.vue)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)

## Node Details View (NDV)

The Node Details View is the primary interface for configuring individual workflow nodes. It provides parameter inputs, data visualization, and execution controls within a sliding panel interface.

### NDV Component Structure

### NDV Actions and Interactions

The NDV supports comprehensive node configuration through typed actions:

| Action Category | NDV Methods | Purpose |
| --- | --- | --- |
| Execution | `NDV.actions.execute()`, `NDV.actions.executePrevious()` | Test node execution |
| Data Management | `NDV.actions.pinData()`, `NDV.actions.setPinnedData()` | Pin execution results |
| Parameter Input | `NDV.actions.typeIntoParameterInput()`, `NDV.actions.clearParameterInput()` | Configure node parameters |
| View Switching | `NDV.actions.switchInputMode()`, `NDV.actions.switchOutputMode()` | Change data display format |
| Expression Editing | `NDV.actions.openInlineExpressionEditor()`, `NDV.actions.validateExpressionPreview()` | Edit expressions |

Sources:
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)

## Parameter Input System

The parameter input system handles dynamic form generation for node configuration, supporting various input types and validation patterns.

### Parameter Input Components

Sources:
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)

## State Management System

The application uses Pinia stores to manage global state across components. Each store follows the Composition API pattern and handles specific domain areas.

### Core Store Architecture

### Settings Store Configuration

The `useSettingsStore` manages frontend configuration and enterprise feature flags:

| Configuration Area | Store Properties | API Source |
| --- | --- | --- |
| Enterprise Features | `isEnterpriseFeatureEnabled` | `/rest/settings` endpoint |
| Deployment Type | `deploymentType`, `isCloudDeployment` | `FrontendSettings.deployment` |
| Authentication | `isLdapLoginEnabled`, `isSamlLoginEnabled` | `FrontendSettings.sso` |
| AI Features | `isAiAssistantEnabled`, `isAskAiEnabled` | `FrontendSettings.aiAssistant` |
| Templates | `isTemplatesEnabled`, `templatesHost` | `FrontendSettings.templates` |

Sources:
- [packages/frontend/editor-ui/src/stores/settings.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/settings.store.ts)
- [packages/frontend/editor-ui/src/stores/users.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/users.store.ts)
- [packages/frontend/editor-ui/src/stores/ui.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/ui.store.ts)

## Data Visualization Components

The UI provides multiple views for displaying and interacting with workflow execution data, supporting different visualization modes and data exploration patterns.

### Run Data Display Modes

### Data Search and Filtering

The data visualization system supports comprehensive search and filtering capabilities:

| Feature | Implementation | Test Coverage |
| --- | --- | --- |
| Text Search | `ndv-search` component | Search across JSON/Table data |
| Schema Search | Schema field filtering | Type-ahead field search |
| Data Highlighting | Mark.js integration | Search term highlighting |
| Pagination | `ndv-data-pagination` | Large dataset handling |
| Item Count Display | `ndv-items-count` | Result count indicators |

Sources:
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)

## Modal and Dialog System

The UI implements a centralized modal system for managing dialogs and overlays throughout the application.

### Modal System Architecture

The system defines over 35 different modal types as constants, enabling type-safe modal management across the application.

Sources:
- [packages/frontend/editor-ui/src/constants.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/constants.ts)
- [packages/frontend/editor-ui/src/stores/ui.store.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/stores/ui.store.ts)
- [packages/frontend/editor-ui/src/Interface.ts](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/Interface.ts)

## Workflow Canvas and Editor

The main workflow editor provides a visual canvas for building and editing workflows with drag-and-drop functionality and real-time execution feedback.

### Canvas Component Architecture

### Canvas Interaction Patterns

The workflow canvas supports comprehensive interaction patterns for workflow building:

| Interaction Type | Implementation | Test Coverage |
| --- | --- | --- |
| Node Addition | `WorkflowPage.actions.addNodeToCanvas()` | Add nodes via plus button or node creator |
| Node Deletion | Context menu + keyboard shortcuts | Delete individual or multiple nodes |
| Node Movement | Drag and drop with position tracking | Real-time position updates |
| Connection Management | Drag between endpoints | Create, delete, and modify connections |
| Canvas Navigation | Zoom, pan, fit-to-screen | Viewport transformation controls |
| Node Execution | Context menu execution | Test individual nodes |

Sources:
- [packages/frontend/editor-ui/src/views/NodeView.vue](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/editor-ui/src/views/NodeView.vue)
- [cypress/pages/workflow.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/workflow.ts)
- [cypress/e2e/12-canvas.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/12-canvas.cy.ts)

## Expression Editor System

The expression editor provides sophisticated support for dynamic expressions and code editing within node parameters.

### Expression Editor Components

Sources:
- [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
- [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
- [cypress/e2e/11-inline-expression-editor.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/11-inline-expression-editor.cy.ts)