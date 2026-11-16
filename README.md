<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=26&duration=3000&pause=1000&color=70A5FD&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=130&lines=Hi+%F0%9F%91%8B+I%27m+soyo;%E4%BD%A0%E5%A5%BD%EF%BC%8C%E6%88%91%E6%98%AF+soyo;Voice+Agents+%7C+Legal+RAG+%7C+AIoT)](https://git.io/typing-svg)

**AI 应用落地生产：延迟 · 容量 · 超时 · 隐私**  
**Production engineering for LLM apps: latency, capacity, timeouts, privacy**

</div>

---

## 关于我 · About Me

AI 应用工程师，2 年经验，从 Java 后端起步。最近半年参与两个项目：AIoT 实时语音 Agent 平台，我独立负责后端与运行时；多人团队里的涉外法律 AI，我负责检索与合同审查。开源项目有 [AgentSandbox](https://github.com/LURENYUANSHI/agent-sandbox)。

AI application engineer with 2 years of experience, starting from Java backends. Over the last six months I have worked on two projects: a realtime voice agent platform for AIoT devices, where I am the sole owner of the backend and runtime, and a cross-border legal AI product on a multi-person team, where I own retrieval and contract review. My open-source work includes [AgentSandbox](https://github.com/LURENYUANSHI/agent-sandbox).

**我关注**：可控的 Agent 执行 · 可追溯的检索与生成 · 完整的产品体验 · 有测试与评审把关的 AI 协作开发  
**I care about:** controlled agent execution · traceable retrieval and generation · end-to-end product experience · AI-assisted engineering backed by tests and review

---

## 代表工作 · Highlights

### 🎙️ AIoT 实时语音 Agent 平台 · Realtime Voice Agent Platform for AIoT

**我的角色**：公司项目，已在国内上线。独立负责 Go 后端与 Python 语音运行时，并用 C 编写 RTL8730E 联调固件（Wi-Fi、Opus 音频、唤醒词、打断），打通设备到平台的实时会话  
**Role:** company project, in production in mainland China. Sole owner of the Go backend and the Python voice runtime; also wrote RTL8730E integration firmware in C (Wi-Fi, Opus audio, wake word, barge-in) that connects the device to live platform sessions

- **两种语音模式，支持打断**：半双工（流式识别 → 文本大模型 → 双向流式合成）与端到端实时语音模型，按键与开口都能打断  
  **Two voice modes with barge-in:** half-duplex (streaming ASR → text LLM → bidirectional streaming TTS) and an end-to-end realtime speech model, interruptible by button or by speaking
- **记忆改为按需调用的工具**：原来每轮都先等记忆召回（实测 0.4–1 s）。改成模型需要时才调用的工具后，Langfuse 统计 75 轮文字对话：57 轮不调工具，首 token 延迟中位数 0.67 s；12 轮查笔记，多一次模型往返，中位数 1.69 s；其余 6 轮调用了记忆召回或多个工具  
  **Memory became an on-demand tool:** every turn used to wait for memory recall first (measured at 0.4–1 s). With recall as a tool the model calls only when needed, Langfuse over 75 text turns shows 57 turns with no tool call at a median time to first token of 0.67 s; the 12 turns that searched notes paid one extra model round trip, at a median of 1.69 s; the other 6 called memory recall or several tools
- **用数据选定 PostgreSQL 而不是 Milvus**：自建 118 条标注查询，Recall@8 为 0.956 对 0.962，配对自助抽样的 95% 区间包含 0；每账户 5 万条记忆时召回 SQL（不含向量化与重排）中位 106 ms。留在 PostgreSQL，免去双写和跨库删除的一致性问题  
  **Chose PostgreSQL over Milvus on data:** on a 118-query labeled set, Recall@8 was 0.956 vs 0.962, with a paired-bootstrap 95% interval that includes 0, and the recall SQL (excluding embedding and rerank) took a median 106 ms at 50,000 memories per account. Staying on PostgreSQL avoided dual writes and cross-store delete consistency
- **GIL 瓶颈：8 核单机约 5 路 → 拆多实例，目标 12 路（实施中）**：单会话约 0.4 核，其中约 0.2 核在 Python 线程里；所有会话共用一个进程和一个 GIL，5 路就占满 GIL 能用的约 1 核。审计限制并发的 11 个环节后设计多实例拆分，同一方案还包括：没有空闲实例时 6 s 内返回 429（现在设备要干等 30 s），发布时逐实例排空  
  **GIL ceiling: about 5 sessions on an 8-core host → multi-instance split targeting 12 (in progress):** a session uses about 0.4 cores, about 0.2 of it in Python threads; with every session in one process sharing one GIL, 5 sessions use up the roughly 1 core a GIL allows. After auditing 11 concurrency bottlenecks, I designed a multi-instance split that also returns a 429 within 6 s when no instance is free (today the device waits 30 s) and drains instances one by one on deploy
- **写库成功的事件不丢**：Go 模块化单体（13 个业务模块，同一二进制按 `api` / `event-worker` / `workflow-worker` 部署），经 gRPC 调用 Python 运行时；模块间用事件解耦，事务性 outbox 把写库成功的事件可靠投递到 Kafka；集成测试直连真实 PostgreSQL，不靠 mock  
  **No lost events after a committed write:** a modular Go monolith (13 business modules, one binary deployed as `api`, `event-worker`, or `workflow-worker`) that calls the Python runtime over gRPC; modules are decoupled by events, a transactional outbox reliably delivers every committed write's event to Kafka, and integration tests run against a real PostgreSQL instead of mocks

### ⚖️ 涉外法律 AI · Cross-border Legal AI

**我的角色**：公司项目，多人团队，负责检索与合同审查  
**Role:** company project on a multi-person team; owner of retrieval and contract review

- **长合同不再因一段超时整体失败**：自研 map-reduce 工作流节点，分段并发、分段结果 Redis 缓存、每段独立超时；21 页合同实测 262–388 s 跑完全流程  
  **Long contracts no longer fail on one slow segment:** a custom map-reduce workflow node with concurrent segments, Redis-cached segment results, and a timeout per segment; a 21-page contract runs end to end in 262–388 s
- **让超时保护重新生效**：LiteLLM 内部重试会把单次 120 s 超时放大到约 360 s，绕过外层超时；内部重试设为 0，由调用方显式重试  
  **Made timeout guards hold again:** LiteLLM's internal retries stretched a 120 s timeout to about 360 s and slipped past the outer guards; internal retries are now 0 and callers retry explicitly
- **混合检索：RRF 融合 + 单文档限额与空位回填**：BM25 + kNN 用 RRF 融合，并限制单篇文档的名额。最初的硬上限没有回填，只有一篇相关文档时 top-5 只剩 2 条；加上空位回填后恢复 5 条。法规按国家分库、可按国家检索，标题精确加权正确处理土耳其语带点 İ 等 Unicode 陷阱  
  **Hybrid retrieval with RRF, per-document caps, and backfill:** BM25 and kNN fused with RRF, with a cap on slots per document. The first hard cap had no backfill, so a query with one relevant document got only 2 of its top 5; adding backfill restored all 5. Laws are split into per-country bases searchable by country, and the exact-title boost handles Unicode traps such as the Turkish dotted İ
- **送审前两层脱敏**：规则层覆盖证件号、统一社会信用代码、银行账号等 20 类字段，模型层再识别人名与公司名，统一换成语义占位符  
  **Two-layer redaction before review:** rules cover 20 field types such as ID numbers, unified social credit codes, and bank accounts, then a model pass finds people's and company names, and everything becomes semantic placeholders
- **律师直接在 Word 里改**：修订建议导出为 Word 原生修订（`w:del` / `w:ins`），逐条接受或拒绝  
  **Lawyers work straight in Word:** suggestions export as native Word tracked changes (`w:del` / `w:ins`), to accept or reject one by one

---

## 开源 · Open Source

<table>
<tr>
<td valign="top">
<strong><a href="https://github.com/LURENYUANSHI/agent-sandbox">AgentSandbox</a> | AI Agent 执行沙箱 · An execution sandbox for AI agents</strong>
<br/><br/>
Agent 每次文件、网络、进程操作前按 YAML 规则（allow / deny）做权限判定；执行轨迹写入 SQLite，可按 trace 回放；单个沙箱限制磁盘与进程数。提供 MCP Server、Python SDK 和可视化控制台，v0.3.0 测试覆盖率 84.3%，CI 与发布流水线齐全。
<br/><br/>
Every file, network, and process action an agent takes is checked against YAML allow/deny rules; execution traces are stored in SQLite and can be replayed by trace; each sandbox has disk and process limits. It ships an MCP server, a Python SDK, and a visual dashboard, with 84.3% test coverage at v0.3.0 and CI and release pipelines.
<br/><br/>
<code>Go</code> <code>Gin</code> <code>React</code> <code>TypeScript</code> <code>MCP</code> <code>OpenTelemetry</code> <code>SQLite</code>
</td>
</tr>
</table>

---

## 技术栈 · Tech Stack

<table>
<tr>
<td align="center" width="50%">

### Agent 与 RAG · Agent & RAG
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=flat-square&logo=elasticsearch&logoColor=white)

`Tool Calling` `Hybrid Search` `Map-Reduce` `LiteLLM` `MCP` `Langfuse`

</td>
<td align="center" width="50%">

### 后端与平台 · Backend & Platform
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

`gRPC` `Outbox` `pgvector` `sqlc` `OpenTelemetry` `Java / Spring Boot`

</td>
</tr>
<tr>
<td align="center" width="50%">

### 实时语音与 AIoT · Realtime Voice & AIoT
![WebSocket](https://img.shields.io/badge/WebSocket-333333?style=flat-square)
![软硬结合 · Hardware + Software](https://img.shields.io/badge/%E8%BD%AF%E7%A1%AC%E7%BB%93%E5%90%88_%C2%B7_Hardware_%2B_Software-FF6F00?style=flat-square)
![C](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=black)

`Streaming ASR / TTS` `Barge-in` `KWS` `RTOS`

</td>
<td align="center" width="50%">

### 前端与工程 · Frontend & DevOps
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

`Vite` `GitHub Actions`

</td>
</tr>
</table>

---

## 贡献 · Contributions

<div align="center">

![snake](https://raw.githubusercontent.com/LURENYUANSHI/LURENYUANSHI/output/github-contribution-grid-snake-dark.svg#gh-dark-mode-only)
![snake](https://raw.githubusercontent.com/LURENYUANSHI/LURENYUANSHI/output/github-contribution-grid-snake.svg#gh-light-mode-only)

欢迎通过公开项目的 Issues 交流技术问题与改进建议。  
Questions and suggestions are welcome through the issues on my public projects.

</div>
