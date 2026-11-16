<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=26&duration=3000&pause=1000&color=70A5FD&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=130&lines=Hi+%F0%9F%91%8B+I%27m+soyo;%E4%BD%A0%E5%A5%BD%EF%BC%8C%E6%88%91%E6%98%AF+soyo;Voice+Agents+%7C+Legal+RAG+%7C+AIoT)](https://git.io/typing-svg)

**AI 应用落地生产：延迟 · 容量 · 超时 · 隐私**  
**Production engineering for LLM apps: latency, capacity, timeouts, privacy**

</div>

---

## 关于我 · About Me

AI 应用工程师，2 年经验，从 Java 后端起步，专注语音 Agent、RAG 与长文档审查的落地。开源项目：[AgentSandbox](https://github.com/LURENYUANSHI/agent-sandbox)。  
AI application engineer with 2 years of experience, starting from Java backends, focused on shipping voice agents, RAG, and long-document review. Open source: [AgentSandbox](https://github.com/LURENYUANSHI/agent-sandbox).

**我关注**：可控的 Agent 执行 · 可追溯的检索与生成 · 完整的产品体验 · 有测试与评审把关的 AI 协作开发  
**I care about:** controlled agent execution · traceable retrieval and generation · end-to-end product experience · AI-assisted engineering backed by tests and review

---

## 代表工作 · Highlights

### 🎙️ AIoT 实时语音 Agent 平台 · Realtime Voice Agent Platform

**我的角色**：已在国内上线；独立负责 Go 后端与 Python 语音运行时，并用 C 编写设备联调固件  
**Role:** live in mainland China; sole owner of the Go backend and Python voice runtime, plus the device integration firmware in C

- 半双工与端到端两种语音模式，支持打断  
  Half-duplex and end-to-end voice modes, both with barge-in
- 记忆改为按需调用的工具，不调工具的轮次首 token 中位 0.67 s  
  Memory recall as an on-demand tool; turns without tools reach the first token in a median 0.67 s
- 用 118 条标注查询对比 pgvector 与 Milvus，召回率无显著差异，留在 PostgreSQL  
  Compared pgvector with Milvus on 118 labeled queries; no significant recall gap, so recall stayed on PostgreSQL
- 定位单进程 GIL 瓶颈（8 核约 5 路），设计多实例扩展到 12 路（实施中）  
  Found a single-process GIL ceiling (about 5 sessions per 8-core host) and designed a multi-instance split targeting 12 (in progress)
- Go 模块化单体，事务性 outbox + Kafka 保证事件不丢  
  A modular Go monolith where a transactional outbox with Kafka keeps events from being lost

### ⚖️ 涉外法律 AI · Cross-border Legal AI

**我的角色**：多人团队中负责检索与合同审查  
**Role:** owner of retrieval and contract review on a multi-person team

- 长合同 map-reduce 审查，分段缓存、独立超时，一段超时不再拖垮整份  
  Map-reduce review of long contracts with cached segments and per-segment timeouts, so one slow segment can't sink the whole review
- 关掉 LiteLLM 内部重试，避免超时被放大约 3 倍  
  Turned off LiteLLM's internal retries so timeouts no longer stretch about 3×
- BM25 + kNN 的 RRF 混合检索，单文档限额 + 空位回填  
  RRF hybrid search over BM25 and kNN, with per-document caps and backfill
- 送审前两层脱敏（规则 + 模型），修订建议导出为 Word 修订稿  
  Two-layer redaction (rules plus a model) before review; suggestions export as Word tracked changes

---

## 开源 · Open Source

**[AgentSandbox](https://github.com/LURENYUANSHI/agent-sandbox)**：AI Agent 执行沙箱，每次文件、网络、进程操作前按 YAML 规则做权限判定，执行轨迹可回放；提供 MCP Server 与 Python SDK，测试覆盖率 84.3%  
**[AgentSandbox](https://github.com/LURENYUANSHI/agent-sandbox):** an execution sandbox for AI agents that checks every file, network, and process action against YAML rules and records replayable traces; ships an MCP server and a Python SDK, with 84.3% test coverage

`Go` `Gin` `React` `TypeScript` `MCP` `OpenTelemetry` `SQLite`

---

## 技术栈 · Tech Stack

<table>
<tr>
<td align="center" width="50%">

### Agent 与 RAG · Agent & RAG
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=flat-square&logo=elasticsearch&logoColor=white)

`Tool Calling` `Hybrid Search` `LiteLLM` `MCP` `Langfuse`

</td>
<td align="center" width="50%">

### 后端与平台 · Backend & Platform
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

`gRPC` `pgvector` `sqlc` `Java / Spring Boot`

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

`Vite` `GitHub Actions` `OpenTelemetry`

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
