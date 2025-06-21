Relevant source files
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

The Workflow Execution Engine is the core orchestrator responsible for executing n8n workflows across different modes and environments. It manages the entire execution lifecycle from initial invocation through completion, handling both direct execution and distributed queue-based processing. The engine coordinates workflow execution, manages active executions, handles scaling across multiple workers, and provides recovery mechanisms for failed executions.

For information about workflow definitions and node execution, see [Node System](https://deepwiki.com/n8n-io/n8n/3-node-system). For configuration and deployment aspects, see [Configuration and Deployment](https://deepwiki.com/n8n-io/n8n/5-configuration-and-deployment).

Execution Modes
---------------

The n8n execution engine operates in two primary modes, configured via the `executions.mode` setting:

| Mode | Description | Use Case |
| --- | --- | --- |
| `regular` | Direct execution in the main process | Single-instance deployments, development |
| `queue` | Distributed execution via Redis queue | Production, horizontal scaling, load distribution |

The mode determines how the `WorkflowRunner` processes execution requests and affects the entire execution pipeline.

Sources: [packages/cli/src/workflow-runner.ts 45](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/workflow-runner.ts#L45-L45)[packages/cli/src/scaling/scaling.service.ts 1-516](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/scaling.service.ts#L1-L516)

Core Architecture
-----------------

The `WorkflowRunner` serves as the primary orchestrator, deciding between direct execution and queue-based execution. The `ActiveExecutions` service tracks all executions in the current process, while the `ScalingService` manages distributed execution via Redis queues.

Sources: [packages/cli/src/workflow-runner.ts 42-455](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/workflow-runner.ts#L42-L455)[packages/cli/src/active-executions.ts 24-233](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/active-executions.ts#L24-L233)[packages/cli/src/scaling/scaling.service.ts 38-515](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/scaling.service.ts#L38-L515)

Execution Flow
--------------

The execution flow begins with the `WorkflowRunner.run()` method, which first registers the execution with `ActiveExecutions.add()`. Based on the execution mode, it either processes directly via `runMainProcess()` or enqueues via `ScalingService.addJob()`.

Sources: [packages/cli/src/workflow-runner.ts 131-196](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/workflow-runner.ts#L131-L196)[packages/cli/src/workflow-runner.ts 199-334](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/workflow-runner.ts#L199-L334)[packages/cli/src/scaling/job-processor.ts 48-248](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/job-processor.ts#L48-L248)

Active Execution Management
---------------------------

The `ActiveExecutions` service maintains a registry of all currently running executions in the process:

Each execution is tracked with:

*   **executionData**: Complete workflow execution context
*   **postExecutePromise**: Promise that resolves when execution completes
*   **workflowExecution**: Cancelable execution promise for stopping
*   **responsePromise**: For webhook response handling

Sources: [packages/cli/src/active-executions.ts 28-30](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/active-executions.ts#L28-L30)[packages/cli/src/interfaces.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/interfaces.ts)

Queue-Based Scaling
-------------------

In queue mode, the `ScalingService` coordinates distributed execution:

The main process enqueues jobs via `ScalingService.addJob()`, while worker processes use `JobProcessor.processJob()` to execute them. Communication happens through Bull's Redis-based pubsub system.

Sources: [packages/cli/src/scaling/scaling.service.ts 184-201](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/scaling.service.ts#L184-L201)[packages/cli/src/scaling/job-processor.ts 48-248](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/job-processor.ts#L48-L248)[packages/cli/src/scaling/scaling.types.ts 1-75](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/scaling/scaling.types.ts#L1-L75)

Execution Lifecycle Hooks
-------------------------

The `ExecutionLifecycleHooks` system provides extensibility throughout execution:

| Hook | Purpose | Timing |
| --- | --- | --- |
| `workflowExecuteBefore` | Pre-execution setup | Before workflow starts |
| `nodeExecuteBefore` | Pre-node setup | Before each node executes |
| `nodeExecuteAfter` | Post-node processing | After each node completes |
| `workflowExecuteAfter` | Post-execution cleanup | After workflow completes |

Different hook configurations are used based on execution context:

*   `getLifecycleHooksForRegularMain()`: Direct execution in main process
*   `getLifecycleHooksForScalingMain()`: Queue mode in main process
*   `getLifecycleHooksForScalingWorker()`: Queue mode in worker process
*   `getLifecycleHooksForSubExecutions()`: Subworkflow executions

Sources: [packages/cli/src/execution-lifecycle/execution-lifecycle-hooks.ts 37-429](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/execution-lifecycle/execution-lifecycle-hooks.ts#L37-L429)

Recovery and Error Handling
---------------------------

The `ExecutionRecoveryService` handles crashed execution recovery:

Recovery works by:

1.   **Log Analysis**: Examining event logs to determine execution state
2.   **State Reconstruction**: Building execution data from available information
3.   **Status Updates**: Marking executions as `crashed` when recovery is needed
4.   **Hook Execution**: Running appropriate lifecycle hooks for cleanup

Sources: [packages/cli/src/executions/execution-recovery.service.ts 22-210](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/executions/execution-recovery.service.ts#L22-L210)

Wait and Resume Mechanism
-------------------------

The `WaitTracker` manages workflow executions that pause and resume:

Wait nodes can pause execution until:

*   **Time expires**: Using `waitTill` timestamp
*   **Webhook called**: External system triggers resume
*   **Manual trigger**: User manually resumes execution

Sources: [packages/cli/src/wait-tracker.ts 13-147](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/wait-tracker.ts#L13-L147)[packages/cli/src/webhooks/waiting-webhooks.ts 34-231](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/webhooks/waiting-webhooks.ts#L34-L231)