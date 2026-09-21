# Agent 核心循环的实现与上下文构成

## R — 原文

> "消息列表中每条消息都有一个角色标识……system、user、assistant、tool。此外,工具定义(tools)作为请求的独立字段。" —— 第 2 章 2.2.1

> "这段代码的核心逻辑只有一个 while 循环和一个判断:模型返回了 tool_calls 就执行工具并继续循环,没有就输出结果并退出。" —— 第 2 章 2.2.4

## I — 阐释

Agent 的最小实现是一个无状态循环:每次把完整消息列表发给模型,模型要么返回最终文本(循环结束),要么返回工具调用请求(框架执行工具、把结果以 tool 角色追加回消息列表,再调一次模型)。上下文由"静态前缀"(系统提示词+工具定义,每次相同)和"轨迹"(user/assistant/tool 消息,只增不减)两部分构成。四个关键协议约束:assistant 的 tool_calls 与 tool 的 tool_call_id 必须配对;工具定义在顶层 tools 字段而非消息;模型只做决策,框架负责执行;生产代码必须有 max_iterations 上限。把握"上下文=消息列表"这一底座,后续所有上下文工程技术(状态栏/压缩/Skills)都只是在优化这个列表的内容和结构。

## A1 — 书中案例

worked_example(第 2 章 2.2.3): 用户问"温哥华当前时间和天气"——第 1 次调用模型并行返回 get_current_time 与 get_weather 两个工具调用;框架执行后把两条 tool 结果连同全部历史重新发送;第 2 次模型给出最终回复。全书用此例展示完整请求/响应 JSON 结构。另: 实验 2-3(第 2 章)证明违反协议的代价——把工具结果伪装成 user 消息会触发 Chat Template 的"换话题"清理,破坏思维链保留,导致重复调用与格式错误。

## A2 — 触发场景

- 从零写一个 Agent / chatbot 后端 / 工具调用 demo,问"Agent 的核心循环怎么写"
- 调试工具调用:模型反复调用同一工具、消息配对报错、思维链莫名被清空
- 审查他人 Agent 代码:发现自拼 "USER: ... ASSISTANT: ..." 字符串、无迭代上限
- 语言信号: "agent core loop", "tool calling", "ReAct 循环", "messages 结构", "为什么模型记不住上一轮"
- 区分: 上下文布局优化(缓存/压缩)见 kv-cache-context-layout 与 context-compression;本卡只管循环正确性与消息协议

## E — 执行步骤

1. 定义消息列表初始态: `[{role:"system", content:身份与规则}, {role:"user", content:任务}]`。完成标准: system 恰好一条且在最前。
2. 定义工具: 顶层 `tools` 字段,每项含 name、description(何时用+边界)、parameters(JSON Schema 含类型与示例)。完成标准: 无工具塞进消息列表。
3. 写循环: `while iterations < max_iterations:` 调模型→追加 assistant 消息(无论文本还是 tool_calls)→若无 tool_calls 则打印并 break→否则逐个执行工具,以 `{role:"tool", tool_call_id, content}` 追加。完成标准: 每条 tool 消息能通过 tool_call_id 关联到请求。
4. 加防护: max_iterations(默认 20-50);工具执行 try/except,异常以结构化错误文本作为 tool 结果返回(不中断会话)。
5. 验证: 跑一个需 2 次以上工具调用的任务,逐步打印 messages 列表,检查四角色配对、只增不改、退出条件。

输入契约: 模型 API 端点、至少 1 个可执行工具、任务文本。输出契约: 最终回复文本 + 完整轨迹。缺失处理: 无可执行工具时只建对话循环并声明无行动能力,不假装调用。

## B — 边界

- 不要在本卡范围内做 KV Cache 布局或压缩(另有卡);不要为省 token 把轨迹转纯文本(实验 2-3 证明这是最具破坏性的模式)
- 模型 API 无状态: "模型记住上次对话"永远是框架重发消息列表的错觉
- 原书警告: 缺工具结果反馈时 Agent 会盲目重试到耗尽预算(实验 1-1);"给出回答"不等于"完成任务"
- 现代模型差异: 部分厂商强制回传 reasoning_content(如 DeepSeek V4 带 tools 时)、thinking block 签名校验(Claude)——跨厂商前查最新文档,多轮对话细节策略演变快
- 本卡的循环是基础形态;异步打断、并行流式等增强见 async-event-agent 与 coding-agent-harness
