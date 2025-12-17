# 编码原则与阶段指南 / Coding Principles & Phase Guide

## 目标 / Goal
- 在不同编码阶段提供一致的决策准则，避免不必要变更，优先交付可验证价值 / Provide consistent decision rules across phases, avoid unnecessary changes, and prioritize verifiable value

## 总体原则 / Core Principles
- 非必要不修改：除非有明确收益（修复问题、提升效率、降低风险、增强可维护性） / Do not change unless necessary: clear benefits only (fix issues, improve efficiency, reduce risk, enhance maintainability)
- 明确收益驱动：改动前说明为何改、度量何种收益 / Benefit-driven: explain why and measurable gains
- 可验证与可回滚：小步、可验证、可回滚 / Verifiable and rollbackable: small, testable changes
- 一致性优先：遵循既有约定与风格 / Consistency first: follow existing conventions and style
- 安全与合规：数据安全、权限、审计与合规优先 / Security & compliance: data safety, access control, audit, compliance
- 渐进式交付：先跑通最小路径，再迭代优化 / Incremental delivery: ship minimal path then iterate

## 阶段指南 / Phase Guide

### 1. 需求澄清与方案设计 / Discovery & Design
- 定义目标与成功度量 / Define goals and success metrics
- 明确范围与非功能性约束 / Clarify scope and non-functional constraints
- 识别风险与假设，制定最小可行方案 / Identify risks/assumptions; design MVP/spike
- 产出验收标准与验证计划 / Produce acceptance criteria and validation plan

### 2. 新功能实现 / New Feature Implementation
- 竖线跑通：先打通主链路 / Vertical slice: wire end-to-end first
- 接口契约优先，保持向后兼容 / Contract-first, backward compatible
- 小步提交与可观测性 / Small commits and observability
- 保护性测试覆盖核心路径 / Protective tests on core paths

### 3. 修改现有代码（谨慎） / Modify Existing Code (Careful)
- 最小化改动、避免顺手重构 / Minimal changes, avoid opportunistic refactors
- 明确收益、可度量提升 / Clear, measurable benefit required
- 边界内变更、收敛影响范围 / Contain impact within module/interface boundaries
- 增量验证与针对性回归 / Incremental validation with targeted regressions

### 4. 重构 / Refactoring
- 先覆盖后重构（测试/观测） / Establish coverage then refactor
- 分离关注点、降低耦合与复杂度 / Separate concerns, reduce coupling/complexity
- 设定度量（复杂度、性能、构建时间） / Set metrics (complexity, performance, build time)
- 分阶段推进、稳定接口 / Phase work with stable interfaces

### 5. 缺陷修复 / Bug Fixes
- 先复现再修复、保留回归用例 / Reproduce before fixing; keep regression tests
- 控制范围、只修问题本身 / Scope strictly to the issue
- 根因分析与复盘记录 / Root cause analysis and postmortem
- 加观测点防止复发 / Add observability to prevent recurrence

### 6. 性能优化 / Performance Optimization
- 数据驱动：Profile/指标定位瓶颈 / Data-driven: profile/metrics locate bottlenecks
- 成本收益权衡与可维护性 / Weigh cost/benefit and maintainability
- 基准与回归保护 / Baselines and regression protection
- 渐进式、可测量优化 / Incremental, measurable improvements

### 7. 依赖升级与外部集成 / Dependencies & Integrations
- 阅读变更日志与迁移指南 / Read changelog and migration guide
- 影子环境/灰度验证，逐步升级 / Shadow/canary validation; gradual upgrades
- 兼容层与降级策略保持生产稳定 / Compatibility layers & graceful degradation
- 锁版本与回滚预案 / Lock versions with rollback plan

### 8. 安全与配置 / Security & Configuration
- 秘钥管理与最小权限 / Secrets management & least privilege
- 输入校验与输出编码 / Input validation & output encoding
- 审计与告警、异常处置流程 / Auditing & alerts, incident handling
- 分环境配置，避免误用 / Environment separation to avoid misconfig

### 9. 测试与质量 / Testing & Quality
- 分层测试：单元/集成/端到端/契约 / Layered testing: unit/integration/e2e/contract
- 质量优先：关键路径有效覆盖 / Quality first: effective key-path coverage
- 不确定性控制（时间/网络/并发） / Control nondeterminism (time/network/concurrency)
- CI 阻断门：关键检查失败阻断合并 / CI gates: block merges on critical failures

### 10. 发布与回滚 / Release & Rollback
- 蓝绿/灰度发布与特性开关 / Blue-green/canary releases & feature flags
- 数据迁移可回滚（双写/版本化） / Rollbackable migrations (dual-write/versioning)
- 运行手册与值班策略 / Runbooks and on-call strategy
- 明确回滚步骤与验证 / Clear rollback steps and validation

### 11. 观测与运维 / Observability & Operations
- 日志分级与结构化 / Structured, leveled logging
- 指标与告警阈值合理设置 / Metrics with sane thresholds
- 错误预算与 SLO 指导节奏 / Error budgets & SLOs guide iteration pace
- 控制噪声与漏报 / Control noise and false negatives

### 12. 文档与沉淀 / Documentation & Knowledge
- 维护变更日志与设计决策记录（ADR） / Maintain changelogs and ADRs
- 更新 README/接口文档，支持自助使用 / Keep README/API docs current; enable self-service
- 上线复盘、沉淀最佳实践 / Release retrospectives and best practices
- 问题库与排错手册 / Issue knowledge base and troubleshooting guide

## 决策检查清单 / Decision Checklist
- 修改前六问：目的/收益/影响范围/验证方法/回滚方案/时间窗口 / Six pre-change questions: purpose, benefit, blast radius, validation, rollback, window
- PR 自检：问题说明与收益、最小化 diff、测试与文档、回滚说明 / PR self-check: clarity & benefit, minimal diff, tests/docs, rollback notes
- 风险评估：是否涉及安全、数据一致性、跨域/跨模块联动 / Risk assessment: security, data consistency, cross-domain/module coupling

## 例外情况 / Exceptions
- 安全漏洞、生产宕机、数据丢失风险、法律合规事件可触发非常规变更 / Security incidents, outages, data loss, compliance trigger exceptional changes
- 采用“快速修复 + 事后重构与复盘”的双步策略 / Use “quick fix + post-refactor/postmortem” two-step strategy

## 防御性编程 / Defensive Programming
- 输入校验与边界检查（类型、范围、长度、格式） / Validate inputs and bounds (type, range, length, format)
- Fail-fast 与清晰错误消息 / Fail fast with clear, actionable error messages
- 不信任外部依赖；设计超时、降级与重试上限 / Do not trust external systems; design timeouts, graceful degradation, and retry caps
- 幂等与可重试路径；避免副作用重复执行 / Ensure idempotency and retryable paths; avoid duplicated side effects
- 资源生命周期管理（连接、文件、锁）；及时释放 / Manage resource lifecycles (connections, files, locks); release promptly
- 不变性优先与最小共享状态；隔离副作用 / Prefer immutability and minimal shared state; isolate side effects
- 空值、异常与错误码统一约定 / Unify policies for nulls, exceptions, and error codes
- 安全默认与最小权限；避免默认开放 / Secure by default and least privilege; avoid default-open configurations
- 结构化日志、关联 ID 与采样；可观测性优先 / Structured logs, correlation IDs, and sampling; prioritize observability
- 断言用于开发与测试；生产采用防御性分支 / Use assertions in dev/test; defensive branches in production
- 限流、熔断、隔离舱保护关键路径 / Apply rate limiting, circuit breakers, and bulkheads on critical paths
- 输入输出契约版本化；兼容演进 / Version I/O contracts; evolve with backward compatibility

## 保守型变更 / Conservative Changes
- 非必要不修改；收益驱动（明确问题或可度量提升） / Do not change unless necessary; benefit-driven (clear problem or measurable gain)
- 最小改动单元与可回滚；小步验证 / Use smallest change units with rollback; verify incrementally
- 在模块/接口边界内收敛影响范围 / Contain impact within module/interface boundaries
- 先覆盖再修改（测试与观测） / Establish tests/observability before modification
- 向后兼容与契约稳定；双栈过渡 / Maintain backward compatibility and stable contracts; dual-stack transitions
- 配置化与特性开关；灰度发布 / Use configuration and feature flags; canary/gradual rollout
- 风险窗口与值班安排；变更审查 / Plan change windows and on-call coverage; enforce change reviews
- 数据迁移版本化与双写；可回滚 / Versioned data migrations with dual-write; ensure reversibility
- 文档与 ADR 持续记录；变更可追溯 / Maintain documentation and ADRs; ensure change traceability
- 复盘与根因追踪；持续改进 / Conduct postmortems and root cause analysis; drive continuous improvement

## 术语对照 / Terms Glossary
- 防御性编程 / Defensive Programming
- 保守型变更 / Conservative Changes
- 非必要不修改 / Do Not Change Unless Necessary
- 竖线跑通 / Vertical Slice
- 契约测试 / Contract Testing
- 幂等 / Idempotency
- 降级 / Graceful Degradation
- 熔断 / Circuit Breaker
- 限流 / Rate Limiting
- 可观测性 / Observability
- 影子环境 / Shadow Environment
- 灰度发布 / Gradual Rollout
- 双写 / Dual-Write
- 版本化 / Versioning
- 回滚 / Rollback
- 特性开关 / Feature Flag
