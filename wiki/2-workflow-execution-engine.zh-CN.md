相关源文件
*   [packages/cli/src/__tests__/workflow-execute-additional-data.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/__tests__/workflow-execute-additional-data.test.ts)
*   [packages/cli/src/__tests__/workflow-runner.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/__tests__/workflow-runner.test.ts)
*   [packages/cli/src/eventbus/event-message-classes/event-message-node.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/eventbus/event-message-classes/event-message-node.ts)
*   [packages/cli/src/eventbus/event-message-classes/event-message-queue.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/eventbus/event-message-classes/event-message-queue.ts)
*   [packages/cli/src/eventbus/event-message-classes/index.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/eventbus/event-message-classes/index.ts)
*   [packages/cli/src/eventbus/message-event-bus/message-event-bus.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/eventbus/message-event-bus/message-event-bus.ts)
*   [packages/cli/src/events/__tests__/log-streaming-event-relay.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/events/__tests__/log-streaming-event-relay.test.ts)
*   [packages/cli/src/events/maps/relay.event-map.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/events/maps/relay.event-map.ts)
*   [packages/cli/src/events/relays/log-streaming.event-relay.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/events/relays/log-streaming.event-relay.ts)
*   [packages/cli/src/execution-lifecycle/__tests__/execution-lifecycle-hooks.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/execution-lifecycle/__tests__/execution-lifecycle-hooks.test.ts)
*   [packages/cli/src/execution-lifecycle/execution-lifecycle-hooks.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/execution-lifecycle/execution-lifecycle-hooks.ts)
*   [packages/cli/src/executions/__tests__/constants.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/executions/__tests__/constants.ts)
*   [packages/cli/src/executions/__tests__/execution-recovery.service.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/executions/__tests__/execution-recovery.service.test.ts)
*   [packages/cli/src/executions/__tests__/utils.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/executions/__tests__/utils.ts)
*   [packages/cli/src/executions/execution-recovery.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/executions/execution-recovery.service.ts)
*   [packages/cli/src/scaling/__tests__/job-processor.service.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/__tests__/job-processor.service.test.ts)
*   [packages/cli/src/scaling/__tests__/scaling.service.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/__tests__/scaling.service.test.ts)
*   [packages/cli/src/scaling/job-processor.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/job-processor.ts)
*   [packages/cli/src/scaling/scaling.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/scaling.service.ts)
*   [packages/cli/src/scaling/scaling.types.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/scaling.types.ts)
*   [packages/cli/src/webhooks/__tests__/waiting-forms.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/webhooks/__tests__/waiting-forms.test.ts)
*   [packages/cli/src/webhooks/__tests__/waiting-webhooks.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/webhooks/__tests__/waiting-webhooks.test.ts)
*   [packages/cli/src/webhooks/waiting-forms.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/webhooks/waiting-forms.ts)
*   [packages/cli/src/webhooks/waiting-webhooks.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/webhooks/waiting-webhooks.ts)
*   [packages/cli/src/workflow-execute-additional-data.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/workflow-execute-additional-data.ts)
*   [packages/cli/src/workflow-runner.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/workflow-runner.ts)
*   [packages/core/test/helpers/constants.ts](https://github.com/xionghao1012/n8n/blob/master/packages/core/test/helpers/constants.ts)
*   [packages/core/test/helpers/index.ts](https://github.com/xionghao1012/n8n/blob/master/packages/core/test/helpers/index.ts)
*   [packages/frontend/@n8n/i18n/src/locales/en.json](https://github.com/xionghao1012/n8n/blob/master/packages/frontend/@n8n/i18n/src/locales/en.json)
*   [packages/workflow/src/message-event-bus.ts](https://github.com/xionghao1012/n8n/blob/master/packages/workflow/src/message-event-bus.ts)

工作流执行引擎是n8n的核心协调器，负责在不同模式和环境下执行工作流。它管理从初始调用到完成的整个执行生命周期，处理直接执行和基于队列的分布式处理。引擎协调工作流执行，管理活动执行，处理多个工作器之间的扩展，并为失败执行提供恢复机制。

有关工作流定义和节点执行的信息，请参阅[节点系统](https://deepwiki.com/n8n-io/n8n/3-node-system)。有关配置和部署方面，请参阅[配置和部署](https://deepwiki.com/n8n-io/n8n/5-configuration-and-deployment)。

执行模式
---------------

n8n执行引擎通过`executions.mode`设置以两种主要模式运行：

| 模式 | 描述 | 使用场景 |
| --- | --- | --- |
| `regular` | 在主进程中直接执行 | 单实例部署，开发环境 |
| `queue` | 通过Redis队列进行分布式执行 | 生产环境，水平扩展，负载分配 |

模式决定了`WorkflowRunner`如何处理执行请求，并影响整个执行管道。

核心架构
----------------

`WorkflowRunner`作为主要协调器，决定是直接执行还是基于队列执行。`ActiveExecutions`服务跟踪当前进程中的所有执行，而`ScalingService`通过Redis队列管理分布式执行。

执行流程
--------------

执行流程从`WorkflowRunner.run()`方法开始，首先通过`ActiveExecutions.add()`注册执行。根据执行模式，它要么通过`runMainProcess()`直接处理，要么通过`ScalingService.addJob()`入队。

活动执行管理
---------------------------

`ActiveExecutions`服务维护当前进程中所有正在运行的执行注册表：

每个执行都跟踪：

*   **executionData**: 完整的工作流执行上下文
*   **postExecutePromise**: 执行完成时解析的Promise
*   **workflowExecution**: 可取消的执行Promise用于停止
*   **responsePromise**: 用于webhook响应处理

基于队列的扩展
-------------------

在队列模式下，`ScalingService`协调分布式执行：

主进程通过`ScalingService.addJob()`将作业入队，而工作进程使用`JobProcessor.processJob()`执行它们。通信通过Bull的基于Redis的pubsub系统进行。

执行生命周期钩子
-------------------------

`ExecutionLifecycleHooks`系统在整个执行过程中提供可扩展性：

| 钩子 | 目的 | 时机 |
| --- | --- | --- |
| `workflowExecuteBefore` | 执行前设置 | 工作流开始前 |
| `nodeExecuteBefore` | 节点执行前设置 | 每个节点执行前 |
| `nodeExecuteAfter` | 节点执行后处理 | 每个节点完成后 |
| `workflowExecuteAfter` | 执行后清理 | 工作流完成后 |

根据执行上下文使用不同的钩子配置：

*   `getLifecycleHooksForRegularMain()`: 主进程中的直接执行
*   `getLifecycleHooksForScalingMain()`: 主进程中的队列模式
*   `getLifecycleHooksForScalingWorker()`: 工作进程中的队列模式
*   `getLifecycleHooksForSubExecutions()`: 子工作流执行

恢复和错误处理
---------------------------

`ExecutionRecoveryService`处理崩溃的执行恢复：

恢复工作通过：

1.   **日志分析**: 检查事件日志以确定执行状态
2.   **状态重建**: 从可用信息构建执行数据
3.   **状态更新**: 当需要恢复时将执行标记为`crashed`
4.   **钩子执行**: 运行适当的生命周期钩子进行清理

等待和恢复机制
-------------------------

`WaitTracker`管理暂停和恢复的工作流执行：

等待节点可以暂停执行直到：

*   **时间到期**: 使用`waitTill`时间戳
*   **Webhook调用**: 外部系统触发恢复
*   **手动触发**: 用户手动恢复执行