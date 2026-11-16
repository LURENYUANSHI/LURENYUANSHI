<div align="center">

<!-- Typing SVG Header -->
[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=28&duration=3000&pause=1000&color=70A5FD&center=true&vCenter=true&multiline=true&repeat=true&width=800&height=130&lines=Hi+%F0%9F%91%8B+I%27m+soyo;%E4%BD%A0%E5%A5%BD%EF%BC%8C%E6%88%91%E6%98%AF+soyo;AI+Agent+%7C+RAG+%7C+AIoT)](https://git.io/typing-svg)

<img height="150" src="https://streak-stats.demolab.com/?user=LURENYUANSHI&theme=tokyonight&hide_border=true" />

</div>

---

## 关于我 · About Me

- AI 应用工程师，2 年经验：从 Java 后端起步 → **AI 应用全栈**  
  AI application engineer, 2 years in: from Java backends to **full-stack AI apps**
- **Agent 与 RAG**：工作流编排、混合检索、工具调用与 MCP  
  **Agents & RAG:** workflow orchestration, hybrid search, tool calling, and MCP
- **法律 AI**：涉外法律工作台的检索与合同审查  
  **Legal AI:** retrieval and contract review for a cross-border legal workbench
- **软硬结合**：嵌入式设备与云端 Agent 的实时语音交互  
  **Hardware + software:** realtime voice between embedded devices and cloud agents

---

## 技术栈 · Tech Stack

<table>
<tr>
<td align="center" width="50%">

### Agent 与 RAG · Agent & RAG
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=flat-square&logo=elasticsearch&logoColor=white)

`Agentic RAG` `Hybrid Search` `Map-Reduce` `LiteLLM` `MCP`

</td>
<td align="center" width="50%">

### 后端与平台 · Backend & Platform
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

`gRPC` `pgvector` `sqlc` `OpenTelemetry`

</td>
</tr>
<tr>
<td align="center" width="50%">

### AIoT 与软硬结合 · AIoT & Hardware
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

`Vite` `GitHub Actions` `CI/CD`

</td>
</tr>
</table>

---

## 项目精选 · Featured Projects

> **涉外法律工作台**：从合同进来到 Word 修订稿出去的完整审查链路。  
> **Cross-border Legal Workbench:** a full review pipeline, from a contract coming in to Word tracked changes going out.

<table>
<thead>
<tr>
<th align="center">脱敏 / Redact</th>
<th align="center">检索 / Retrieve</th>
<th align="center">审查 / Review</th>
<th align="center">交付 / Deliver</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">规则 + 模型两层脱敏<br/><sub>Rule + model redaction</sub></td>
<td align="center">BM25 + kNN 混合检索<br/><sub>Hybrid search with RRF</sub><br/>按国家分库<br/><sub>Per-country law bases</sub></td>
<td align="center">长合同 map-reduce 审查<br/><sub>Map-reduce review of long contracts</sub><br/>分段缓存与超时<br/><sub>Per-segment cache & timeouts</sub></td>
<td align="center">Word 原生修订稿<br/><sub>Native Word tracked changes</sub></td>
</tr>
</tbody>
</table>

<table>
<tr>
<td width="50%" valign="top">
<strong>涉外法律工作台 · Cross-border Legal Workbench</strong>
<br/><sub>公司产品 · Company product</sub>
<br/><br/>
面向涉外法律的 AI 工作台，我负责检索与合同审查：长合同分段审查、送审前脱敏、修订建议直接导出为 Word 修订稿。
<br/><br/>
An AI workbench for cross-border legal work, where I own retrieval and contract review: segmented review of long contracts, redaction before review, and suggestions exported straight to Word tracked changes.
<br/><br/>
<code>FastAPI</code> <code>React</code> <code>Elasticsearch</code> <code>Redis</code> <code>LiteLLM</code>
</td>
<td width="50%" valign="top">
<strong><a href="https://github.com/LURENYUANSHI/agent-sandbox">AgentSandbox</a> | AI Agent 执行沙箱 · Execution Sandbox</strong>
<br/><sub>开源 · Open source</sub>
<br/><br/>
每次文件、网络、进程操作前按 YAML 规则做权限判定，执行轨迹可回放，提供 MCP Server 与 Python SDK。
<br/><br/>
Checks every file, network, and process action against YAML rules, records replayable traces, and ships an MCP server and a Python SDK.
<br/><br/>
<code>Go</code> <code>Gin</code> <code>React</code> <code>MCP</code> <code>SQLite</code>
</td>
</tr>
</table>

---

## 动态 · Activity Graph

<div align="center">

[![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=LURENYUANSHI&theme=tokyo-night&hide_border=true&area=true)](https://github.com/ashutosh00710/github-readme-activity-graph)

</div>

---

## 贡献 · Contribution Snake

<div align="center">

![snake gif](https://raw.githubusercontent.com/LURENYUANSHI/LURENYUANSHI/output/github-contribution-grid-snake-dark.svg#gh-dark-mode-only)
![snake gif](https://raw.githubusercontent.com/LURENYUANSHI/LURENYUANSHI/output/github-contribution-grid-snake.svg#gh-light-mode-only)

</div>
