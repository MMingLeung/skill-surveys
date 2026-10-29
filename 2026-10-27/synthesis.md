# 2026-10-27 综述

当日阅读 5 个仓库。星标为当日 GitHub API `stargazers_count`。Browserbase 仓库根没有 SPDX，抽查的技能目录标明 MIT，详见该篇。SkillCorpus 仓库内没有 `SKILL.md`，有策展、检索、评测和给代理看的安装说明，因此保留，没有换仓库。

| 笔记 | 仓库 | 星标 | 许可（查阅所见） | 类型 |
| --- | --- | --- | --- | --- |
| [browser-use.md](browser-use.md) | [browser-use/browser-use](https://github.com/browser-use/browser-use) | 119276 | MIT | 浏览器代理库，附 6 个技能 |
| [browserbase-skills.md](browserbase-skills.md) | [browserbase/skills](https://github.com/browserbase/skills) | 3745 | 仓库 SPDX 未设置；抽查技能为 MIT | 官方浏览器技能包（18 个技能目录） |
| [planning-with-files.md](planning-with-files.md) | [OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files) | 27701 | MIT | 文件计划与可选完成门 |
| [genoffice.md](genoffice.md) | [genspark-ai/genoffice](https://github.com/genspark-ai/genoffice) | 11049 | Apache-2.0；`ee/` 为企业许可，笔记未使用 | 真实 Office 文件的命令与技能 |
| [skillcorpus.md](skillcorpus.md) | [EverMind-AI/SkillCorpus](https://github.com/EverMind-AI/SkillCorpus) | 692 | 主代码 Apache-2.0；`match/`、`evaluate/`、`lifecycle/` 为 MIT；语料保留上游许可 | 技能语料、检索与评测 |

## 写法上的共同点

五份材料都把走错路写在走对路旁边。Browser Use 的库文档、云 API、直接操作浏览器互相写明不要用谁。Browserbase 把本机和远端、开浏览器和直接抓取分成不同技能。GenOffice 的命令表有一列「不要用这条」。Planning with Files 写了跳过简单问答和单文件修改。SkillCorpus 的检索门宁可不选。

第二处共同点是完成不看模型自己说。QA 技能先看任务走没走完，总分取最弱的关键路径，并要求证据。界面测试技能要求操作前后各留一次页面状态。提示优化技能要求有一次不再改提示的确认跑。GenOffice 要求读检查输出、看渲染页面，并写明检查命令可以成功退出却仍带着问题。Planning with Files 的门看磁盘上的计划文件，不看对话。

第三处是入口短、细则在旁边。浏览器库的两份技能是「主题到文件」的表。GenOffice 让操作字段去读由校验器生成的说明，避免技能正文和命令各写一套。计划技能把模板和脚本放在规则旁边。SkillCorpus 默认只索引名字和 description，正文不进搜索面。

第四处是外部文字不当成指令。计划技能把网页结果放进发现文件，不放进会被钩子重读的计划。浏览器技能在登录、密码和支付前停下。GenOffice 不允许把办公文件当压缩包拆开读。

## 设计意图

这些仓库默认模型会过早打开浏览器，会把退出码 0 说成文档已完成，会在上下文被压缩后忘掉计划，也会在 description 含糊时加载错误技能。所以规则写成路由、停手条件和文件上的证据。

技能数量用不同办法压住。Browser Use 和 Browserbase 靠互相指向的负例。Planning with Files 把持久化收成三个固定文件，而不是宿主里的待办列表。GenOffice 把 42 个文书放在推荐目录，命令技能只有一份。SkillCorpus 在检索端只留 0 到 2 条，并把模型已经会做的步骤退役。

本库八个技能是交付过程。这五个仓库分别是浏览器产品、云端技能包、宿主钩子、办公引擎和语料管道，不替换那八个名字。

## 对本库可抄的部分

可抄的是纪律，落在已有文件上，不新开技能名。

1. **浏览器入口保持「不必打开」和「登录就停」。** `drission-crawler` 继续写：能直接请求的不开浏览器；要交互或登录态才打开。站点差异先读站点包。登录、验证码、提交仍交给使用人。
2. **一次只改一个假设，再用当次回读。** 站点包改选择器时不在同一轮叠加多条。失败落盘。同一失败不原样重试，几次之后停下来问人。
3. **检查输出和页面都要看。** `dev-review-verify` 维持 LIVE 在最后。若检查脚本把问题写在输出里却成功退出，收工要读那份输出。多页 DEMO 里一条必需路径失败，整次不算通过。结论仍是验收完成或未验收完成。
4. **文档路由写清不负责什么。** `work-doc-writer` 先判定文种再打开模板。扫描件读到空文本时写明没识别到文字。未知事实标待确认，讨论倾向不写成已决定。
5. **description 写使用人会说的话。** 触发样本留在各技能 `evals.json`。新增顶层技能前先看会不会挡住已有描述。模型不看技能也会做的泛泛步骤，不另开技能。

## 对本库不抄的部分

1. **不换浏览器产品。** 不把 `drission-crawler` 换成 Browser Use 或 Browserbase 的命令、云端浏览器、登录态同步、验证码代理，或自动改写技能的循环。
2. **不换办公引擎。** 不把 GenOffice 的命令表、操作名、推荐文书或 `ee/` 企业版代码写入 `work-doc-writer`、`word-thesis-format`。不接会离开本机的搜索、生图和音视频理解。
3. **不装计划钩子和停止门。** 开工卡保持一页四块。不生成三份计划文件。Cursor 在来源文档里不是硬拦截宿主。页面原文不和禁止项放进同一份自动重读的文件。
4. **不建技能语料库。** 不引入检索模型、策展流水线、三维质量分或每轮自动注入。论文里的通过率不进入验收标准。
5. **不把外部技能正文贴进本库。** Browserbase 仓库根许可未设置。SkillCorpus 的语料保留上游许可。两边都只记结构。

## 若以后改现有技能，优先动哪里

本次只记阅读结论，不改 `skills/`。

- `drission-crawler`：description 保持「能请求就不打开浏览器」。站点包一次改一个原因。回读落在证据文件。登录和提交的停手不变。
- `dev-review-verify`：读检查脚本的输出，不只看退出码。必需路径有一条失败就不写验收完成。不引入 1 到 5 分或 HTML 报告。
- `work-doc-writer`：文种判断旁边保持「不负责哪一种」。待确认保持原样。不替换模板。
- `word-thesis-format`：版式完成仍以预览为准。不改走外部办公 CLI。
- `demo-kickoff-card`：保持四块。长任务不另加三文件计划。
- `dev-process-handoff`：写行为、默认值、验收变化，以及这次用的检查脚本版本。不写个人风格，也不写技能退役接口。
- `government-service-design`：不增加界面评分维度或方案竞选。
- `windows-gui-bat-launcher`：就绪仍看窗口和标志文件。不改成办公软件或浏览器云端的启动方式。
