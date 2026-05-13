# 🌌 PhaseShard Engine

PhaseShard 是一个基于离线大语言模型（LLM Agent）与原生 D3.js 物理引擎构建的自动化知识图谱系统。

系统采用了严格的 **Producer-Consumer（生产者-消费者）** 解耦架构：通过 Python 后端（Producer）对本地 Markdown 知识库（如 Obsidian）进行 AST 感知级别的语义提取，并输出标准 JSON；通过纯前端 Vite/Vue 页面（Consumer）进行高性能的拓扑可视化。

## 🏗️ System Architecture

PhaseShard 引擎被划分为两个完全独立、可通过单一数据契约 (`phaseshard.json`) 联动的子系统：

1. **Agent Backend (Producer):**
   * **输入**: 本地 Markdown 文件夹。
   * **引擎**: Python + LLM 模型
   * **机制**: 采用 **Actor-Critic 范式**的 RAG 工作流。AST 分块器提取代码边界，Actor 负责特征抽取（摘要与标签），Critic 负责数据合法性校验与反馈重试。
   * **输出**: 写入到前端 `public/` 目录的拓扑数据结构 (`phaseshard.json`)。

2. **Graph Renderer (Consumer):**
   * **栈**: Vite + Vue 3 + D3.js。
   * **呈现**: 纯粹的全屏沉浸式图谱。包含 D3.js 力导向图（Force-Directed Graph）、平滑无闪烁的 CSS 硬件加速渲染、基于 Flexbox 防溢出的多维联动面板，以及双端（Light/Dark）主题切换。

## 📂 Directory Layout

建议的 Monorepo 工程目录结构如下：

```text
VaultGraph-Project-Root/
├── README.md
├── phaseshard.config.yaml     <-- 全局系统配置总线
│
├── agent/                     <-- 🧠 [Producer] Python 分析引擎
│   ├── main.py                <-- 引擎入口，挂载 Config 并分发任务
│   ├── core/
│   │   ├── role.py            <-- Actor/Critic 角色扮演引擎
│   │   ├── ast_chunker.py     <-- AST Markdown 语法树拆分器
│   │   └── llm_provider.py    <-- 模型通信协议层
│   └── requirements.txt
│
└── frontend/                  <-- 👁️ [Consumer] Vite 渲染前端
    ├── package.json
    ├── vite.config.ts
    ├── public/
    │   └── phaseshard.json    <-- ⚠️ Agent 的最终产物必须写入此处
    └── src/
        ├── App.vue            <-- 全局样式重置与容器挂载
        ├── main.ts
        └── components/
            └── PhaseShardGraph.vue  <-- 核心 D3 渲染引擎与 UI 面板
