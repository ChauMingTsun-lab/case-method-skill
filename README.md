# case-method — 案例研究方法论 Agent Skill

> ***政治科学案例研究方法论助手***。基于 Sartori、KKV、George & Bennett、Mahoney & Goertz 等 17 章经典方法论文献构建，提供交互式研究设计引导、方法论自查、章节写作辅助和术语查询。

**English TL;DR**: An agent skill that helps social science researchers design, critique, and write case study research. Four subcommands (`design`/`check`/`write`/`lookup`) grounded in 17 canonical methodology chapters including Sartori (1970), KKV (1994), George & Bennett (2005), and Mahoney & Goertz (2004, 2006).

---

## 为什么做这个 Skill？

案例研究是政治科学领域最易被误用的研究方法之：概念拉伸、DV 选择偏差、忽视等终性、过程追踪被当作"增加 N"……这些错误在方法论文献中被反复讨论。这个 Agent Skill 把 17 章文献的精华浓缩为可供 Claude Code 即时调用的知识库，帮助你：

- **在写方法论章节之前**，用 `/case-method:design` 引导完成研究设计的 13 个关键决策
- **在投稿之前**，用 `/case-method:check` 对照六维度审查研究设计的方法论弱点
- **写作卡壳时**，用 `/case-method:write` 获得规范的方法论段落写作思路和关键引用
- **遇到陌生术语**，用 `/case-method:lookup` 查询定义、来源和学者争论

---

## 四个子命令速览

| 子命令                  | 用途                              | 典型输入                                      |
| ----------------------- | --------------------------------- | --------------------------------------------- |
| `/case-method:design` | 交互式研究设计引导（5 阶段）      | `/case-method:design 我想研究东亚民主化`    |
| `/case-method:check`  | 方法论自查（六维度评估 + 优先级） | 粘贴或描述你的研究设计                        |
| `/case-method:write`  | 方法论章节写作辅助（8 个主题）    | `/case-method:write 过程追踪`               |
| `/case-method:lookup` | 术语与学者争论查询                | `/case-method:lookup conceptual stretching` |

直接提问（不带子命令）也可以——skill 会按问题类型自动路由到对应知识库文件。

---

## 覆盖的方法论主题

- **概念构建与测量**：Sartori 抽象阶梯、概念拉伸、家族相似/辐射范畴、Adcock & Collier 效度框架
- **因果理论**：反事实因果、INUS 因果、等终性、因果机制 vs. 因果效应
- **案例选择与选择偏差**：Lijphart 框架、Geddes 警告、可能性原则（Mahoney & Goertz 2004）、MSSD/MDSD
- **研究方法**：Mill 方法、一致性方法、过程追踪（四类型 + 贝叶斯逻辑）、QCA、关键案例
- **类型学理论**：属性空间、类型学 vs. 类型学理论、四种研究设计
- **学者争论**：KKV vs. George & Bennett、DV 选择合法性、概念修改策略、负面案例、质性 vs. 量化方法地位

完整索引见 [`case-method/SKILL.md`](case-method/SKILL.md)；各主题深度展开见 [`case-method/references/`](case-method/references/)。

---

## 安装

本 skill 由两部分组成：**skill 本体**（`case-method/` 目录，含 SKILL.md 与 references）和**配套 slash 命令**（`.claude/commands/case-method/` 目录，提供 `/case-method:design` 等快捷入口）。两部分需要分别复制到对应位置。

### 方法一：git clone（推荐，方便跟进更新）

**用户级**（全局可用，所有项目都能触发）：

```bash
git clone https://github.com/ChauMingTsun-lab/case-method-skill.git
cp -r case-method-skill/case-method ~/.claude/skills/
cp -r case-method-skill/.claude/commands/case-method ~/.claude/commands/
```

**项目级**（仅当前项目可用）：

```bash
git clone https://github.com/ChauMingTsun-lab/case-method-skill.git
cp -r case-method-skill/case-method <your-project>/.claude/skills/
cp -r case-method-skill/.claude/commands/case-method <your-project>/.claude/commands/
```

> slash 命令是可选的——不复制也能用（skill 会通过 description 自动触发），但复制后能在 `/` 菜单里看到 4 个 `/case-method:*` 入口，调用更明确。

### 方法二：手动复制粘贴（不用 git）

从 GitHub 右上角 **Code → Download ZIP** 下载整个 repo，解压后按下方路径，把 `case-method/` 和 `.claude/commands/case-method/` 两个目录分别复制到对应位置。

#### Claude Code 官方规范

用户级（全局）：

| 源目录                            | 目标目录                            |
| --------------------------------- | ----------------------------------- |
| `case-method/`                  | `~/.claude/skills/case-method/`   |
| `.claude/commands/case-method/` | `~/.claude/commands/case-method/` |

项目级（单项目）：

| 源目录                            | 目标目录                                         |
| --------------------------------- | ------------------------------------------------ |
| `case-method/`                  | `<your-project>/.claude/skills/case-method/`   |
| `.claude/commands/case-method/` | `<your-project>/.claude/commands/case-method/` |

#### 通用 agent skill 规范

部分 agent 工具链（非 Claude Code 生态）使用 `.agents/skills/` 作为 skill 发现目录。若你的工具链遵循该约定，把 skill 本体目录放到：

```
<your-project>/.agents/skills/case-method/
```

> **路径约定确认**：各 agent 工具对 skill 发现路径的支持并不统一——Claude Code 读取 `.claude/skills/`，部分其他工具读取 `.agents/skills/`。请先确认你使用的工具实际扫描哪个路径，再选择对应位置。slash commands（`.claude/commands/`）目前是 Claude Code 特有概念，其他 agent 工具链可能没有对等机制。

### 验证安装

在 Claude Code 中输入：

```
/case-method:lookup 概念拉伸
```

若返回 Sartori (1970) 的定义、核心要点和相关概念，说明 skill 已正确加载。如果 `/case-method:*` 斜杠命令没出现在 `/` 菜单中，检查 `.claude/commands/case-method/` 是否复制到位（或重启 Claude Code 让其重新扫描命令目录）。

---

## 设计原则

这个 skill 遵循 Anthropic 官方 [skill-creator](https://github.com/anthropics/skills) 的最佳实践：

1. **渐进披露（Progressive Disclosure）**：SKILL.md 仅 288 行（约 1100 字），内联高频决策表；长篇展开放在 8 个 `references/` 文件中，按需读取，不浪费上下文。
2. **触发词丰富**：frontmatter 的 description 包含中英文混合触发词（`案例研究`、`case study method`、`过程追踪`、`process tracing`、`KKV`、`MSSD/MDSD` 等），保证各类表述都能命中。
3. **每个 references 文件都有 TOC**：长文件顶部有目录，Claude 可快速预览全貌而不必全文加载。
4. **对立观点平衡呈现**：学者存在分歧处（如 DV 选择合法性、负面案例选择）呈现多方立场而非单方采信。
5. **方法论工具，不越俎代庖**：帮助用户做出方法论上站得住脚的选择，不替用户做实质性理论判断。

---

## 测试

skill 附带 4 个测试场景剧本 [`examples/test-scenarios.md`](examples/test-scenarios.md)，覆盖：

1. 子命令路由正确性（design）
2. check 的六维度完整性（DV 选择偏差识别）
3. lookup 的中英混合匹配
4. 无子命令的被动路由

你可以在自己的 Claude Code 会话中跑这些剧本，对照预期行为验证 skill 是否正常。

---

## 知识库来源（17 章核心文献）

**概念与测量类**

- Sartori (1970) "Concept Misformation in Comparative Politics"
- Collier & Mahon (1993) "Conceptual 'Stretching' Revisited"
- Adcock & Collier (2001) "Measurement Validity"

**因果与方法论类**

- King, Keohane & Verba (1994) *Designing Social Inquiry* (Ch. 3, 4)
- Mahoney & Goertz (2006) "A Tale of Two Cultures"
- George & Bennett (2005) *Case Studies and Theory Development* (Ch. 1, 8, 9, 10, 11)

**案例选择与比较设计类**

- Lijphart (1971) "Comparative Politics and the Comparative Method"
- Collier (1993) "The Comparative Method"
- Geddes (1990) "How the Cases You Choose Affect the Answers You Get"
- Collier & Mahoney (1996) "Insights and Pitfalls"
- Mahoney & Goertz (2004) "The Possibility Principle"
- Lange, Mahoney & vom Hau (2006) "Colonialism and Development"

**覆盖范围说明**：本 skill 聚焦截至 2006 年的经典文献。后续发展如 Beach & Pedersen (2013) 的过程追踪新分类、Schneider & Wagemann (2012) 的集合论方法**未被涵盖**。

完整参考文献见 [`case-method/references/07_术语表与学者争论.md`](case-method/references/07_术语表与学者争论.md) 第 7.3 节。

---

## 反馈与贡献

本 skill 当前版本 **v1.0.0**（完整变更记录见 [CHANGELOG.md](CHANGELOG.md)）。欢迎通过以下方式反馈：

- **发现方法论错误**：开 [Issue](https://github.com/ChauMingTsun-lab/case-method-skill/issues)，注明哪一条建议与哪位学者的原文冲突
- **补充缺失主题**：Pull Request，新增 references 文件或扩充 SKILL.md 的决策表
- **使用体验问题**：Issue 中注明 skill 在你的研究设计中的触发情境、预期 vs. 实际行为

**目前已知的覆盖缺口**：

- 过程追踪的新分类（Beach & Pedersen 2013）
- QCA 的系统化讨论（Schneider & Wagemann 2012）
- 多方法设计（nested analysis, Lieberman 2005）

---

## License

[MIT](LICENSE) — 可自由使用、修改、分发。**但是**：本 skill 的内容是对已发表学术文献的综合整理，引用时请标注原始文献（如 Sartori 1970 而非本 skill）。

---

## 作者

Chau Ming Tsun · [ChauMingTsun-lab](https://github.com/ChauMingTsun-lab)

如果这个 skill 对你的研究有帮助，考虑在论文致谢中提及或给 repo 加一颗 ⭐️。
