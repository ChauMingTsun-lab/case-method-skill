# Changelog

本文件记录 `case-method` skill 的所有重要变更。格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)。

## [1.0.0] — 2026-04-22

### 初始公开发布

**核心功能**

- 四个原生 slash 命令：`/case-method:design`（研究设计引导）、`/case-method:check`（方法论自查）、`/case-method:write`（章节写作辅助）、`/case-method:lookup`（术语查询）——通过 `.claude/commands/case-method/*.md` 注册到 Claude Code 的命名空间命令菜单
- 8 个主题知识库文件：总览、概念构建与测量、因果关系理论、案例选择与选择偏差、研究方法（过程追踪与一致性）、类型学理论与研究设计、实操指南、术语表与学者争论
- 基于 17 章经典方法论文献构建（Sartori 1970、Collier & Mahon 1993、Adcock & Collier 2001、KKV 1994 Ch.3-4、Mahoney & Goertz 2006、Lijphart 1971、Collier 1993、Geddes 1990、Collier & Mahoney 1996、Mahoney & Goertz 2004、George & Bennett 2005 Ch.1/8/9/10/11、Lange/Mahoney/vom Hau 2006）

**设计合规性（对照 Anthropic 官方 skill-creator 最佳实践）**

- SKILL.md 约 1100 字（远低于 500 行建议上限），内联高频决策表；低频详细内容放入 `references/` 按需读取，避免上下文浪费
- 每个 >100 行的 references 文件顶部均有 TOC（目录），支持 Claude 快速预览全貌而不必全文加载
- `description` 字段含丰富的中英混合触发词，兼顾各种表述
- 对立观点平衡呈现：学者分歧处（如 DV 选择合法性、负面案例选择、概念修改策略）呈现多方立场而非单方采信

**安装路径**

- 支持 Claude Code 官方约定：`.claude/skills/` + `.claude/commands/`（用户级 `~/.claude/` 或项目级 `<project>/.claude/`）
- 兼容通用 agent skill 约定：`.agents/skills/`（适用于遵循该约定的非 Claude Code 工具链；slash 命令为 Claude Code 特有）

**文档**

- `README.md`：中英双语，完整安装/使用/测试/反馈流程
- `LICENSE`：MIT（含学术引用说明——skill 内容来自已发表学术文献，引用请标注原始文献）
- `examples/test-scenarios.md`：4 个测试场景剧本，供用户验证 skill 触发、路由、输出格式

### 已知局限

- 覆盖范围截至 2006 年经典文献。以下后续发展**未被涵盖**：
  - 过程追踪新分类（Beach & Pedersen 2013）
  - 集合论方法的系统化讨论（Schneider & Wagemann 2012）
  - 多方法设计（nested analysis, Lieberman 2005）
- 目前仅支持简体中文界面，繁体/英文界面未在初始版本提供

### 反馈与贡献

欢迎通过 [GitHub Issues](https://github.com/ChauMingTsun-lab/case-method-skill/issues) 提交 bug 报告、方法论修正或覆盖缺口建议。
