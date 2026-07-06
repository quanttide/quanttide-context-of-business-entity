名称/项目	核心能力	协议/接口	典型适用场景	维护状态
skillc rustcc.cn	技能开发工具链：skc init、lint、build（编译为SQLite FTS5索引）、search、show、stats 技能运行时：提供MCP服务器实现，但核心是文件系统技能管理	文件系统 + 可选 MCP	开发、管理、分发技能包，希望技能能被主流AI工具（如Claude Desktop、Cursor）直接调用	活跃 (2026年更新)
yoagent crates.io	轻量级代理循环：Prompt → LLM流 → 工具执行 → 循环 技能加载：兼容AgentSkills标准，可加载技能目录并注入系统提示	文件系统 + 事件流	需要一个简单、专注的代理循环，并希望其能自动加载和使用本地技能	活跃
SkillLite csdn.net	多入口技能执行引擎：提供CLI、Python SDK、MCP、Desktop、Swarm等多种入口 核心内核：沙箱执行 + 安全扫描 + 技能语义	文件系统 + 多种接口	需要一个可嵌入的、安全的技能执行内核，并希望支持多种集成方式	活跃
awaken-agent lib.rs	统一运行时：一个二进制同时服务AI SDK、AG-UI、A2A、MCP、ACP等多种客户端 技能管理：支持技能的运行时发现和激活	文件系统 + 多协议	需要一个统一的、生产级的智能体运行时，支持技能且需对接多种前端	活跃
MicroClaw csdn.net	全能AI助手：一个Agent打通所有聊天平台 技能系统：兼容Anthropic Agent Skills标准，内置多种技能，支持自定义	文件系统	希望有一个开箱即用的、自带技能系统的完整智能体应用	活跃


