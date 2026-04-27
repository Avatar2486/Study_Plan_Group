# Flowable

---

## 🟢 LEVEL 1 — Flowable Foundations

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| BPMN, Workflow Engine, Process Automation | Understand ProcessEngine and engine bootstrap | Structure of `<definitions>` and executable `<process>` |
| Flowable Architecture (Process, DMN, CMMN, App Engine) | Engine services overview and responsibilities | How different engines deploy their own XML types |
| Process Definition vs Process Instance | RepositoryService vs RuntimeService difference | id, key, and versioning behavior in XML |
| Start → Task → End lifecycle | RuntimeService start APIs, TaskService lifecycle | StartEvent, Task types, EndEvent |

---

## 🟢 LEVEL 2 — BPMN Fundamentals

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| User Task | TaskService lifecycle, IdentityService links | `<userTask>` attributes (assignee, candidateUsers, candidateGroups) |
| Service Task | JavaDelegate, delegateExpression resolution | `flowable:class`, `flowable:delegateExpression`, `flowable:type` |
| Script Task | Script execution vs Java delegate difference | `<scriptTask>` and script formats |
| Business Rule Task | DecisionService interaction | `<businessRuleTask>` with decisionRef |
| Exclusive Gateway | Variable evaluation timing | Conditional sequence flows |
| Parallel Gateway | Execution tree branching | Fork and join gateway XML |
| Inclusive Gateway | Conditional parallel paths | Inclusive gateway conditions |
| Event-Based Gateway | Waiting for external triggers | Event definitions tied to gateway |
| Intermediate Events | Catch and throw events, timer/message/signal/error/escalation | `<intermediateCatchEvent>` and `<intermediateThrowEvent>` |
| ReceiveTask / SendTask | RuntimeService signal or message APIs | `<receiveTask>` and `<sendTask>` definitions |
| Conditional Events | Variable-driven triggers | `<conditionalEventDefinition>` |

---

## 🟢 LEVEL 3 — Subprocesses & Advanced BPMN

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Embedded Subprocess | Execution hierarchy | `<subProcess>` structure |
| Call Activity | Process-to-process linking | calledElement and version binding |
| Event Subprocess | Interrupting vs non-interrupting behavior | Event subprocess start event XML, multi-instance event subprocess |
| Ad-hoc Subprocess | Dynamic task activation | Ad-hoc markers in XML |
| Multi-instance | Collection handling in variables, completion conditions | `<multiInstanceLoopCharacteristics>`, sequential vs parallel, element variables |
| Compensation | Compensation handlers, chained compensation | `<compensateEventDefinition>` |

---

## 🟡 LEVEL 4 — Boundary Events

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Timer Boundary | Job creation & scheduling | Timer definitions (duration, date, cycle) |
| Error Boundary | BpmnError vs Exception | `<errorEventDefinition>` |
| Signal Boundary | Broadcast vs targeted events | `<signalEventDefinition>` |
| Message Boundary | Correlation mechanisms | `<messageEventDefinition>` |
| Escalation | Escalation vs error difference | `<escalationEventDefinition>` |
| SLA Timers | Task/job-level deadlines | Boundary timer events |

---

## 🟡 LEVEL 5 — Runtime Execution Internals

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Execution Tree & Tokens | DelegateExecution hierarchy | How parallel and nested flows appear in XML |
| Execution vs Task vs Instance | RuntimeService vs TaskService entities | Task-producing elements vs pure execution steps |
| Command Pattern | Engine command context lifecycle | N/A (engine internal) |
| Transactions & Wait States | Spring transaction boundaries | Wait state elements (UserTask, ReceiveTask, Timer) |
| Optimistic Locking | Handling concurrent updates | Parallel flows and async continuations |
| Async Boundaries | Async before/after, exclusive vs non-exclusive | asyncBefore, asyncAfter, exclusive flags |

---

## 🟡 LEVEL 6 — Database & Persistence

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| ACT_RE_* tables | Deployment and definition queries | Deployment metadata from XML |
| ACT_RU_* tables | Runtime queries and execution state | XML constructs that create runtime rows |
| ACT_HI_* tables | HistoryService queries | History level impact of BPMN design |
| Variable storage | Serialization formats (JSON, JPA) | Variable usage patterns in expressions |
| Large Objects & JSON | Handling custom objects | Field extensions, input/output mappings |

---

## 🟡 LEVEL 7 — Variables & State Management

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Global vs Local variables | DelegateExecution variable scopes | Variable references in expressions |
| Serialization (JSON, JPA) | Custom object variables | Field extensions and input/output mappings |
| Concurrent updates | Retry behavior on conflicts | Async boundaries affecting variable commits |
| Variable Scoping Edge Cases | Execution vs task vs subprocess variables | XML variable mappings in multi-instance and async |

---

## 🟠 LEVEL 8 — Service Tasks & Integration

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| JavaDelegate vs Expression | Bean resolution | class vs delegateExpression |
| External Worker pattern | External task APIs, fetch-and-lock, retries | External task type configuration |
| Async service tasks | Job executor interaction, async job handling | asyncBefore, asyncAfter, exclusive flags |
| Idempotency | Retry-safe delegate design | Async + exclusive flags |
| Technical vs BPMN errors | Exception mapping | Error event definitions |
| SendTask / ReceiveTask Integration | Send/receive APIs | XML task type attributes |

---

## 🟠 LEVEL 9 — User Tasks & Human Workflow

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Task lifecycle | TaskService state transitions | UserTask definition |
| Assignment & identity links | IdentityService usage, tenant-aware identity queries | assignee, candidates |
| Task listeners | TaskListener interface | TaskListener XML |
| Execution listeners | ExecutionListener interface | ExecutionListener XML |
| Form handling | FormService APIs | `<formKey>` and `<formProperty>` mappings |
| SLA timers | Timer jobs on tasks | Boundary timer events |

---

## 🟠 LEVEL 10 — Events & Event Registry

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Message events | Correlation APIs, tenant-aware events | Message event definitions |
| Signal events | Broadcast mechanics | Signal definitions |
| Event subprocess | Runtime interruption | Event subprocess XML, interrupting/non-interrupting |
| Event registry | Event payload mapping | Event model XML |
| Inbound vs Outbound events | Event dispatching | Event definitions in BPMN |

---

## 🟠 LEVEL 11 — Async, Timers & Job Executor

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Async continuations | Job lifecycle APIs | async attributes |
| Job acquisition | ManagementService job queries | Async task markers |
| Retry mechanism | Failed job handling | Retry cycles via async |
| Dead letter jobs | Moving jobs via APIs | N/A |
| Engine crash recovery | Transaction commit timing | Async boundaries |
| Async Multi-instance / Subprocess | Execution & variable commit behavior | XML async + multi-instance markers |

---

## 🟠 LEVEL 12 — DMN

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Decision tables | DecisionService APIs | DMN XML structure |
| Hit policies | Decision evaluation results, advanced hit policies (COLLECT, RULE_ORDER) | Hit policy attributes |
| BPMN + DMN integration | Passing variables | businessRuleTask, input/output mappings |
| Literal expressions | Evaluating complex expressions | DMN XML literalExpression |

---

## 🟠 LEVEL 13 — CMMN

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Case model | CaseService APIs | CMMN XML |
| Sentries & milestones | Case execution state | Entry/exit criteria XML |
| Discretionary tasks | Dynamic task activation | Discretionary item XML |

---

## 🔴 LEVEL 14 — Performance & Scaling

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Engine clustering | Async executor config, multi-thread tuning | Async-heavy modeling patterns |
| DB tuning | Query patterns, table locking, historic queries | Process design impact on DB |
| History cleanup | HistoryService cleanup jobs | History level settings |
| Long vs short processes | Transaction size impact, variable serialization | Wait state modeling |
| Multi-tenant performance | Tenant-aware queries | tenantId in XML definitions |

---

## 🔴 LEVEL 15 — Security & Multi-Tenancy

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Authentication & Authorization | IdentityService integration, tenant-aware security | Candidate users/groups, tenantId-aware |
| Tenant deployments | Tenant-aware APIs, tenant-specific process definitions | tenantId in deployments |
| Data isolation | Multi-tenant engine config | Tenant separation via definitions |

---

## 🔴 LEVEL 16 — Microservices & Sagas

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Saga orchestration | Service integration patterns, compensation logic | Compensation events |
| Event-driven workflows | Message correlation, idempotent handling | Message start/intermediate events |
| Idempotent calls | Retry-safe logic | Async + boundary errors |
| External task microservices | Worker fetch-and-lock patterns | XML configuration of external task topics |

---

## 🔴 LEVEL 17 — Testing, Debugging & Operations

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Unit testing processes | Flowable test utilities | Testing different BPMN paths, boundary events, multi-instance, async |
| Debugging stuck executions | Runtime & job queries | Async/wait state modeling |
| Recovering failed processes | Job retry APIs, dead letter handling | Error boundary design |
| Observing DB state | Runtime & history queries, variable auditing | XML structures causing state |
| Migration testing | Version upgrades, async/subprocess testing | XML version compatibility |

---

## 🔴 LEVEL 18 — Migration & Versioning

| 🧠 Theory | ☕ Java Focus | 📄 XML Focus |
| --- | --- | --- |
| Definition versioning | RepositoryService queries | Version behavior on redeploy |
| Migrating instances | Migration APIs for subprocess, multi-instance, async tasks | Structural compatibility in XML |
| Rolling upgrades | Deployment strategies | Backward-compatible modeling |
| Multi-instance & Event Subprocess migration | Variable and execution mapping | XML adjustments for complex scenarios |

---