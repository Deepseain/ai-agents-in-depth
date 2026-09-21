# 能力索引（完整版）

| capability_id | 标题 | 重要度 | 意图 | 关键词 | 能力卡 |
|---|---|---|---|---|---|
| cap.ai-agents-in-depth.agent-core-loop | Agent 核心循环的实现与上下文构成 | critical | 从零实现 Agent 核心循环；调试工具调用协议问题；理解上下文的消息构成 | agent core loop、tool calling、ReAct、messages、tool_call_id、核心循环、工具调用 | capabilities/agent-core-loop.md |
| cap.ai-agents-in-depth.kv-cache-context-layout | KV Cache 友好的上下文布局 | critical | 设计上下文布局防止缓存失效；排查首 token 延迟与账单异常；决定动态信息注入位置 | KV Cache、prompt cache、prefix、TTFT、cache hit、前缀缓存、缓存失效 | capabilities/kv-cache-context-layout.md |
| cap.ai-agents-in-depth.system-prompt-design | 流程驱动的系统提示词与工具定义设计 | critical | 从零写系统提示词；修复 Agent 不遵守规则；写工具定义描述；业务规则进提示词 | system prompt、SOP、tool description、few-shot、提示词设计、业务规则 | capabilities/system-prompt-design.md |
| cap.ai-agents-in-depth.prompt-injection-defense | 提示注入的识别与分层防御 | high | 为读外部内容的 Agent 设计安全方案；评估 Agent 攻击面；排查可疑的被劫持行为 | prompt injection、间接注入、data poisoning、guardrails、三层护栏、Agent 安全 | capabilities/prompt-injection-defense.md |
| cap.ai-agents-in-depth.skill-authoring | 编写 Skill：渐进式披露机制与内容结构 | high | 编写 SKILL.md；把领域能力模块化；修复 Skill 误触发或不触发 | SKILL.md、progressive disclosure、渐进式披露、skill 编写、能力包 | capabilities/skill-authoring.md |
| cap.ai-agents-in-depth.agent-status-bar | Agent 状态栏设计与维护 | high | 让 Agent 感知调用计数与约束余量；防长任务目标漂移；注入环境信息而不破坏缓存 | status bar、TODO list、tool call counter、状态栏、计数器 | capabilities/agent-status-bar.md |
| cap.ai-agents-in-depth.context-compression | 上下文压缩策略设计 | high | 控制上下文膨胀；设计压缩策略；排查上下文腐化（装得下但找不到） | context compression、context rot、上下文压缩、摘要、子 Agent 隔离 | capabilities/context-compression.md |
| cap.ai-agents-in-depth.user-memory-system | 用户记忆系统设计 | high | 让 Agent 跨会话记住用户；设计记忆写入与冲突处理；记忆框架选型 | user memory、长期记忆、跨会话、JSON Cards、Mem0、个性化 | capabilities/user-memory-system.md |
| cap.ai-agents-in-depth.rag-pipeline | RAG 管道构建：分块、混合检索、重排序与指标 | high | 从零搭知识库问答；调优检索质量；为 RAG 定验收指标；选分块与重排序策略 | RAG、chunking、hybrid search、BM25、reranker、recall@k、分块、重排序 | capabilities/rag-pipeline.md |
| cap.ai-agents-in-depth.knowledge-base-governance | 知识库更新与治理：PR 审核流、定期整理与权限 | high | 设计知识库写入审核流程；处理知识冲突与过期；多租户知识权限设计 | 知识更新、PR 审核流、proposer-reviewer、定期整理、租户隔离、知识投毒 | capabilities/knowledge-base-governance.md |
| cap.ai-agents-in-depth.agentic-rag | 智能体化 RAG 与上下文感知检索 | medium | 提升多跳复杂问题的检索质量；决定检索控制权策略；修复分块上下文丢失 | agentic RAG、iterative retrieval、多跳检索、contextual retrieval、上下文感知检索 | capabilities/agentic-rag.md |
| cap.ai-agents-in-depth.tool-design-discovery | 工具设计决策与爆炸治理 | high | 决定能力做成工具还是 Skill；写工具描述；治理工具爆炸；接入大量 MCP | tool design、ACI、tool description、MCP、tool discovery、工具膨胀 | capabilities/tool-design-discovery.md |
| cap.ai-agents-in-depth.execution-tool-safety | 执行工具的安全机制栈 | high | 给写删执行类工具设计防误伤；定义人工确认范围；政策类操作的合规裁决设计 | sandbox、sidecar、幂等、审批、不可逆操作、命令注入、服务端真值 | capabilities/execution-tool-safety.md |
| cap.ai-agents-in-depth.coding-agent-harness | Coding Agent 流程与故障恢复 | high | 构建或评估 Coding Agent；设计故障检测恢复与熔断；判断任务适不适合交给 Agent | coding agent、harness、circuit breaker、重试、熔断、轨迹接管、四象限 | capabilities/coding-agent-harness.md |
| cap.ai-agents-in-depth.code-meta-capability | 代码作为元能力的六维应用 | high | 决定该用代码还是生成模型；把业务政策变成不可绕过约束；数据查询走 SQL artifact；让 Agent 生成界面或创建 Agent | code interpreter、生成式 UI、artifact、agent 自举、代码化规则、A2UI | capabilities/code-meta-capability.md |
| cap.ai-agents-in-depth.async-event-agent | 异步事件驱动的 Agent 设计 | medium | 让 Agent 接收外部事件触发；处理执行中的打断与补充；设计异步任务句柄语义 | event-driven、异步、interrupt、打断、消息队列、事件循环 | capabilities/async-event-agent.md |
| cap.ai-agents-in-depth.voice-agent-architecture | 语音 Agent 架构选择 | medium | 选语音 Agent 架构；排查语音延迟与机械感；决定快慢思考是否分离 | voice agent、级联、全双工、VAD、快慢思考、TTFT | capabilities/voice-agent-architecture.md |
| cap.ai-agents-in-depth.computer-use-design | Computer Use：GUI 自动化 Agent 设计 | medium | 自动化无 API 的网页/桌面/手机操作；选视觉定位路线；排查点错位置与页面变化失败 | computer use、GUI 自动化、grounding、Set-of-Mark、元素树、browser agent | capabilities/computer-use-design.md |
| cap.ai-agents-in-depth.eval-fundamentals | 评估体系基础：任务定义、指标口径与数据集设计 | critical | 从零搭 Agent 评估集；定义成功指标口径；设计评估任务与验证器；引用公开基准做决策 | evaluation、benchmark、Pass@k、tau-bench、验证器、用户模拟器、评估数据集 | capabilities/eval-fundamentals.md |
| cap.ai-agents-in-depth.llm-judge-failure-attribution | LLM-as-a-Judge/Rubric 与失败归因 | high | 评估开放式产出质量；定位失败的第一步错误；把问题案例转成回归用例；防 LLM 评判偏差 | LLM as a judge、rubric、failure attribution、首错定位、轨迹前缀、回归任务 | capabilities/llm-judge-failure-attribution.md |
| cap.ai-agents-in-depth.model-selection-cost | 评估驱动的模型选型与成本分析 | high | 决定换不换新模型；定位 Agent 成本构成；判断分数差异是不是噪声；多模型分层策略 | 模型选型、成本分析、TTFT、p95、统计显著性、McNemar、配对比较 | capabilities/model-selection-cost.md |
| cap.ai-agents-in-depth.eval-driven-iteration | 评估驱动的系统改进与内部评估基础设施 | high | 从 benchmark 报告决定下一步改什么；建消融与 AB 测试基础设施；管理提示词版本 | 改进闭环、ablation、AB 测试、feature flag、单变量、提示词版本 | capabilities/eval-driven-iteration.md |
| cap.ai-agents-in-depth.posttraining-selection | Mid-training、SFT 与 RL 的选择决策 | medium | 判断该不该微调或上 RL；规划后训练路线；知识放参数还是 RAG；RL 不收敛排查 | SFT vs RL、LoRA、mid-training、pass@k、微调决策、后训练 | capabilities/posttraining-selection.md |
| cap.ai-agents-in-depth.reward-design-rlvp | 奖励设计与 RLVP：奖励结果、约束过程 | medium | 把任务目标变成 RL 奖励；防 reward hacking；修复组内零方差无梯度 | reward design、RLVR、reward hacking、PRM、RLVP、路径惩罚 | capabilities/reward-design-rlvp.md |
| cap.ai-agents-in-depth.continual-evolution | 持续进化闭环：学习信号、四种载体与验证发布 | high | 建越用越好的自我进化机制；决定经验写进知识/Prompt/程序/参数；设计安全的自我修改流程 | continual learning、持续进化、自我进化、系统提示学习、sleep-time、双循环 | capabilities/continual-evolution.md |
| cap.ai-agents-in-depth.multi-agent-architecture | 多 Agent 架构决策：信息增量与共享×拓扑 | high | 判断要不要拆多 Agent；设计协作架构与通信协议；决定上下文共享还是隔离 | multi-agent、信息增量、提议者-审核者、manager、handoff、移交包 | capabilities/multi-agent-architecture.md |
| cap.ai-agents-in-depth.multi-agent-failure-modes | 多 Agent 六种失败模式与防御 | medium | 多 Agent 上线前风险检查；排查文件覆盖/级联错误/同质重复/互相扯皮/子 Agent 爆炸 | 乐观锁、级联失败、共因失效、理解债、拜占庭、并发冲突 | capabilities/multi-agent-failure-modes.md |
