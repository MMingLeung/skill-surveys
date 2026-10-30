# 2026-10-30 综述

当日阅读 5 个仓库。星标为当日 GitHub API `stargazers_count`。Graphify 的 SPDX 与工程配置是 Apache-2.0，`LICENSE-MIT` 保留再许可前的部分贡献。gstack 整体为 MIT，`NOTICE.md` 另标明部分设计材料的上游许可；本笔记未使用那些设计文件。

第 5 个仓库从替补里选了 Obsidian Skills。它覆盖笔记格式、命令行和「模板加数据出 Markdown」，比技能安全扫描、技能规范更靠近文档交付。安全扫描与同日的审计证据门重叠。规范仓库离办公自动化更远，且 2026-10-26 已读过官方技能库。替补另两仓因此不单写。

| 笔记 | 仓库 | 星标 | 许可（查阅所见） | 类型 |
| --- | --- | --- | --- | --- |
| [gstack.md](gstack.md) | [garrytan/gstack](https://github.com/garrytan/gstack) | 138243 | MIT；部分设计材料另有上游许可，笔记未使用 | 流程技能套件（浏览、测试、评审、发布、评测登记） |
| [graphify.md](graphify.md) | [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 139170 | Apache-2.0；历史部分见 `LICENSE-MIT` | 代码与文档的可查询图 |
| [security-audit-skill.md](security-audit-skill.md) | [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | 53444 | MIT | 多阶段审计与可校验发现记录 |
| [compound-engineering.md](compound-engineering.md) | [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) | 25785 | MIT | 插件：交接、浏览器核实、评审与复利学习 |
| [obsidian-skills.md](obsidian-skills.md) | [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | 50431 | MIT | 笔记格式、命令行与模板渲染 |

## 写法上的共同点

五份材料都把「做完了」写成可以再读的记录。gstack 的浏览报告要有地址、控制台和截图，空的控制台也要留下。安全审计把结局收成可校验的记录，待验证和已确认不是同一档。Compound 的浏览器测试要求每条受影响路径都有通过、失败或带原因的跳过。Graphify 的每条边标明是抽出还是推断。Obsidian 的画布技能在写完后有格式校验清单。

第二处是入口短，细则在旁边，并且写清何时不跑完全程。gstack 用根路由和章节索引。安全审计写明加载技能只是指导，完整审计要明确请求。Compound 的交接和浏览器技能要求先读 `references/` 再动手。Obsidian 的 Markdown 技能只写方言，通用语法不重复。Graphify 把构建原理放在文档里，技能负责何时去查图。

第三处是外部文字不当成指令。页面内容、交接正文、图上的节点说明，都是材料。交接要使用人确认之后才继续。审计记录里看不到的部署行为不允许猜。

第四处是规模差很大，但都试图用路由压住误触发。gstack 和 Compound 是几十个技能的套件。另外三份是单一图技能、单一审计技能和六份笔记技能。本库仍是少数交付技能，不跟着套件的个数增长。

## 设计意图

这些仓库默认模型会把没打开的页面说成测过，会自己宣布问题已证实，会在会话断开后丢掉计划，会把网页或旧交接当成下一步，也会在文档方言上写成普通 Markdown。规则因此落在证据字段、独立核对、指针式交接和「只写模型不会的那一截」。

Graphify 解决的是检索，不是排版，也不是扫描件识别。Obsidian 解决的是笔记库格式和批量渲染。两者都不替换公文模板。

## 对本库可抄的部分

可抄的是纪律，落在已有文件上，不新开技能名。

1. **收工按路径给结论。** `dev-review-verify` 对必需路径逐条写通过、失败或跳过原因。少一条就不写验收完成。检查输出要读。空结果也要写明。
2. **交接是指针。** `dev-process-handoff` 指向开工卡、当次证据和相关文件，并写下一句要看哪里。确认文件已写下。正文不当成操作指令。只有行为、默认值或验收变了才写。
3. **浏览器一次一种方式，登录就停。** `drission-crawler` 不在同一次里混用驱动。登录、验证码和提交交给使用人。页面文字进证据，不进指令。
4. **文档只写方言和出处。** `work-doc-writer` 保持文种路由。引用写明出自哪一份。推断和原文不要同一语气。扫描件没有文字就写没识别到。`word-thesis-format` 仍以预览为完成。
5. **技能加载不等于做完全程。** description 写清何时收工、何时只改文档。意思含糊先问。模型已经会的通用步骤不写进技能正文。

## 对本库不抄的部分

1. **不装流程套件或插件。** 不引入 gstack 的角色团队、发布流水线和付费评测，也不引入 Compound 的 36 个技能。
2. **不换浏览器，不接图和笔记库。** `drission-crawler` 保持现有步骤。不把 Graphify、Obsidian CLI 或网页抽正文写进公文链。
3. **不把安全审计搬进收工。** 不用发现档、严重度、覆盖账本或攻击面分册。缺证据的结论是未验收完成。
4. **不把交接放在临时目录。** 正式交接留在约定位置。权威产物仍是模板、页面和导出文件。
5. **不摘外部正文。** 当日仓库虽是 MIT 或 Apache-2.0，笔记只记结构。gstack 派生设计材料和 Graphify 的历史 MIT 部分都不贴进本库。

## 若以后改现有技能，优先动哪里

本次只记阅读结论，不改 `skills/`。

- `dev-review-verify`：必需路径逐条有结论，跳过写原因。读检查输出。不引入审计裁决或付费评测登记。
- `dev-process-handoff`：指针指向当次证据，写清哪一条行为或验收变了。交接落盘后再算写过。正文不作为下一次的指令。
- `drission-crawler`：一次一种浏览器方式。登录和提交停手。页面文字只进证据。站点包一次改一个原因。
- `work-doc-writer`：文种判断保持。出处和待确认保持。不接图谱、笔记语法或网页抽取。
- `word-thesis-format`：版式完成仍看预览。不改用外部渲染命令。
- `demo-kickoff-card`：保持四块。不改成多角色评审链，也不先建知识图。
- `government-service-design`：不增加外观竞选、画布或设计材料里的派生规则。
- `windows-gui-bat-launcher`：就绪仍看窗口和标志文件。不改成笔记库或办公软件的启动方式。
