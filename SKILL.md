---
name: ai-agents-in-depth
description: |
  《深入理解 AI Agent》（李博杰，v2.0 2026）全书方法论的入口。当用户要构建、调试、评估或改进 LLM Agent 系统时使用：
  写 Agent 核心循环与上下文工程（KV Cache 布局/提示词/Skills/状态栏/压缩）、用户记忆与 RAG 知识库、工具设计与安全护栏、
  Coding Agent 与故障恢复、异步/语音/GUI 交互扩展、评估体系（任务设计/指标口径/LLM-as-a-Judge/失败归因）、模型选型与成本、
  后训练路线（Mid-training/SFT/RL）与奖励设计、持续进化闭环、多 Agent 架构与失败防御。
  不适用于：与 Agent 无关的通用编程问题、具体模型版本的参数咨询、需要真实算力集群的模型训练实操。
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.ai-agents-in-depth
  cangjie.capability-count: 27
  cangjie.entrypoint-count: 1
---
# 深入理解 AI Agent（设计原理与工程实践） — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 与 Agent 无关的通用编程、数学、数据科学问题
- 具体模型版本（如 Kimi K3/GPT-5.6）的参数、定价与 API 细节咨询——书中数据为 2026 年中快照
- 需要真实算力集群的模型训练实操与机器人真机部署（书中相应章节仅为参考）
- Agent 社会/Agent 经济等展望性讨论的具体落地实施

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. Agent = LLM + 上下文 + 工具（大脑+眼睛+手脚），三者缺一不可；模型固定时扩展观察空间与动作空间是最大能力杠杆
2. Harness 是竞争力所在：约束、验证与纠正机制确保 Agent"可靠地做事"，模型能力正在商品化
3. 上下文 = 静态前缀 + 轨迹；静态前缀字节级稳定以命中 KV Cache，动态信息一律追加末尾
4. 五大设计模式贯穿全书：提议者-审核者、渐进式披露、只增不改、边界集+保留集、最小 diff+可回滚
5. 没有评估就没有工程：观察→假设→实验→验证，把 Agent 开发从炼金术变成科学；指标口径由业务风险决定
6. 数据和环境比算法更重要：Mid-training 定底座、SFT 定协议、环境与奖励定 RL 能学到什么
7. 安全是架构问题：护栏按被绕过难度分上下文/执行/数据三层；多 Agent 的价值判据是信息增量

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 从零实现 Agent 核心循环；调试工具调用协议问题；理解上下文的消息构成 | references/capabilities/agent-core-loop.md | references/capabilities/kv-cache-context-layout.md、references/capabilities/system-prompt-design.md、references/capabilities/async-event-agent.md |
| 设计上下文布局防止缓存失效；排查首 token 延迟与账单异常；决定动态信息注入位置 | references/capabilities/kv-cache-context-layout.md | references/capabilities/context-compression.md、references/capabilities/agent-status-bar.md |
| 从零写系统提示词；修复 Agent 不遵守规则；写工具定义描述；业务规则进提示词 | references/capabilities/system-prompt-design.md | references/capabilities/skill-authoring.md、references/capabilities/prompt-injection-defense.md、references/capabilities/tool-design-discovery.md |
| 为读外部内容的 Agent 设计安全方案；评估 Agent 攻击面；排查可疑的被劫持行为 | references/capabilities/prompt-injection-defense.md | references/capabilities/execution-tool-safety.md、references/capabilities/knowledge-base-governance.md |
| 编写 SKILL.md；把领域能力模块化；修复 Skill 误触发或不触发 | references/capabilities/skill-authoring.md | references/capabilities/system-prompt-design.md、references/capabilities/tool-design-discovery.md |
| 让 Agent 感知调用计数与约束余量；防长任务目标漂移；注入环境信息而不破坏缓存 | references/capabilities/agent-status-bar.md | references/capabilities/kv-cache-context-layout.md、references/capabilities/context-compression.md |
| 控制上下文膨胀；设计压缩策略；排查上下文腐化（装得下但找不到） | references/capabilities/context-compression.md | references/capabilities/kv-cache-context-layout.md、references/capabilities/rag-pipeline.md |
| 让 Agent 跨会话记住用户；设计记忆写入与冲突处理；记忆框架选型 | references/capabilities/user-memory-system.md | references/capabilities/rag-pipeline.md、references/capabilities/knowledge-base-governance.md、references/capabilities/continual-evolution.md |
| 从零搭知识库问答；调优检索质量；为 RAG 定验收指标；选分块与重排序策略 | references/capabilities/rag-pipeline.md | references/capabilities/agentic-rag.md、references/capabilities/knowledge-base-governance.md、references/capabilities/user-memory-system.md |
| 设计知识库写入审核流程；处理知识冲突与过期；多租户知识权限设计 | references/capabilities/knowledge-base-governance.md | references/capabilities/rag-pipeline.md、references/capabilities/continual-evolution.md |
| 提升多跳复杂问题的检索质量；决定检索控制权策略；修复分块上下文丢失 | references/capabilities/agentic-rag.md | references/capabilities/rag-pipeline.md、references/capabilities/agent-core-loop.md |
| 决定能力做成工具还是 Skill；写工具描述；治理工具爆炸；接入大量 MCP | references/capabilities/tool-design-discovery.md | references/capabilities/execution-tool-safety.md、references/capabilities/skill-authoring.md |
| 给写删执行类工具设计防误伤；定义人工确认范围；政策类操作的合规裁决设计 | references/capabilities/execution-tool-safety.md | references/capabilities/prompt-injection-defense.md、references/capabilities/tool-design-discovery.md |
| 构建或评估 Coding Agent；设计故障检测恢复与熔断；判断任务适不适合交给 Agent | references/capabilities/coding-agent-harness.md | references/capabilities/execution-tool-safety.md、references/capabilities/eval-driven-iteration.md、references/capabilities/multi-agent-architecture.md |
| 决定该用代码还是生成模型；把业务政策变成不可绕过约束；数据查询走 SQL artifact；让 Agent 生成界面或创建 Agent | references/capabilities/code-meta-capability.md | references/capabilities/execution-tool-safety.md、references/capabilities/multi-agent-architecture.md |
| 让 Agent 接收外部事件触发；处理执行中的打断与补充；设计异步任务句柄语义 | references/capabilities/async-event-agent.md | references/capabilities/agent-core-loop.md、references/capabilities/multi-agent-architecture.md |
| 选语音 Agent 架构；排查语音延迟与机械感；决定快慢思考是否分离 | references/capabilities/voice-agent-architecture.md | references/capabilities/async-event-agent.md |
| 自动化无 API 的网页/桌面/手机操作；选视觉定位路线；排查点错位置与页面变化失败 | references/capabilities/computer-use-design.md | references/capabilities/code-meta-capability.md |
| 从零搭 Agent 评估集；定义成功指标口径；设计评估任务与验证器；引用公开基准做决策 | references/capabilities/eval-fundamentals.md | references/capabilities/llm-judge-failure-attribution.md、references/capabilities/model-selection-cost.md、references/capabilities/eval-driven-iteration.md、references/capabilities/execution-tool-safety.md |
| 评估开放式产出质量；定位失败的第一步错误；把问题案例转成回归用例；防 LLM 评判偏差 | references/capabilities/llm-judge-failure-attribution.md | references/capabilities/eval-fundamentals.md、references/capabilities/eval-driven-iteration.md、references/capabilities/continual-evolution.md |
| 决定换不换新模型；定位 Agent 成本构成；判断分数差异是不是噪声；多模型分层策略 | references/capabilities/model-selection-cost.md | references/capabilities/eval-fundamentals.md、references/capabilities/eval-driven-iteration.md |
| 从 benchmark 报告决定下一步改什么；建消融与 AB 测试基础设施；管理提示词版本 | references/capabilities/eval-driven-iteration.md | references/capabilities/eval-fundamentals.md、references/capabilities/llm-judge-failure-attribution.md、references/capabilities/continual-evolution.md |
| 判断该不该微调或上 RL；规划后训练路线；知识放参数还是 RAG；RL 不收敛排查 | references/capabilities/posttraining-selection.md | references/capabilities/eval-fundamentals.md、references/capabilities/reward-design-rlvp.md、references/capabilities/continual-evolution.md |
| 把任务目标变成 RL 奖励；防 reward hacking；修复组内零方差无梯度 | references/capabilities/reward-design-rlvp.md | references/capabilities/posttraining-selection.md、references/capabilities/llm-judge-failure-attribution.md |
| 建越用越好的自我进化机制；决定经验写进知识/Prompt/程序/参数；设计安全的自我修改流程 | references/capabilities/continual-evolution.md | references/capabilities/llm-judge-failure-attribution.md、references/capabilities/posttraining-selection.md、references/capabilities/user-memory-system.md |
| 判断要不要拆多 Agent；设计协作架构与通信协议；决定上下文共享还是隔离 | references/capabilities/multi-agent-architecture.md | references/capabilities/multi-agent-failure-modes.md、references/capabilities/coding-agent-harness.md |
| 多 Agent 上线前风险检查；排查文件覆盖/级联错误/同质重复/互相扯皮/子 Agent 爆炸 | references/capabilities/multi-agent-failure-modes.md | references/capabilities/multi-agent-architecture.md |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- 请求超出本书能力域（路由表与索引均未命中）时明确告知，不硬套书中方法
- 涉及真实不可逆操作（支付/删除/对外发送）时，只提供书中防御机制的设计，不代为执行
- 需要原书未提供的关键条件（如精确公式/最新厂商策略）时声明缺口并指向 needs-review 记录，不以猜测补齐
