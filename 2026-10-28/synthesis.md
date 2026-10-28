# 2026-10-28 综述

当日阅读 5 个仓库。星标为当日 GitHub API `stargazers_count`。MinerU 的仓库 SPDX 为 NOASSERTION，`LICENSE.md` 是 Apache-2.0 加附加条款，该篇只记思路。Skill Seekers 的默认分支是 `development`。

| 笔记 | 仓库 | 星标 | 许可（查阅所见） | 类型 |
| --- | --- | --- | --- | --- |
| [mineru.md](mineru.md) | [opendatalab/MinerU](https://github.com/opendatalab/MinerU) | 82670 | SPDX 为 NOASSERTION；`LICENSE.md` 为 Apache-2.0 加商业门槛与在线服务署名 | 文档解析器，附一份代理技能 |
| [agent-browser.md](agent-browser.md) | [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser) | 44751 | Apache-2.0 | 浏览器命令行，入口技能是存根，另有评测 |
| [mattpocock-skills.md](mattpocock-skills.md) | [mattpocock/skills](https://github.com/mattpocock/skills) | 305361 | MIT | 可组合的工程技能（含交接、审查、测试） |
| [skillopt.md](skillopt.md) | [microsoft/SkillOpt](https://github.com/microsoft/SkillOpt) | 18732 | MIT | 用留出验证门训练技能正文 |
| [skill-seekers.md](skill-seekers.md) | [yusufkaraaslan/Skill_Seekers](https://github.com/yusufkaraaslan/Skill_Seekers) | 15245 | MIT | 把文档、仓库、PDF 收成技能 |

## 写法上的共同点

五份材料都把「先取得证据」写在「宣布结果」前面。MinerU 要求先解析再摘要，截断了就说明读到哪。agent-browser 要求先有当次快照，再按引用操作。mattpocock 的审查从固定起点看差异，没有规格就写没有规格。SkillOpt 的修改要在留出集上变好才留下。Skill Seekers 在多个来源不一致时做冲突检测，不合成一句。

第二处是入口短，细则跟着会变的东西走。MinerU 的技能先写约定和分叉，安装和质量档放在后面。agent-browser 的 `SKILL.md` 只负责指向已安装版本里的说明。mattpocock 把测试细则放到技能旁边的文件，编排技能禁止模型自己调用。SkillOpt 的 README 把训练步骤指到版本文档。Skill Seekers 的技能按来源类型分流，不把抓取细节写进入口。

第三处是失败要停在人能选择的地方。MinerU 在质量不够或需要把文件送出本机时等人选。agent-browser 在遮挡或不可见时让点击失败，再重新看页面。SkillOpt-Sleep 把改动暂存，等人采用；真实后端会把会话摘录送出，文档要求先审再发。mattpocock 的交接去掉密钥，并指向已有文件，不另写一套事实。

第四处是评测看行为，不看作者自述。agent-browser 用必须出现和不得出现的模式检查有没有先加载技能。SkillOpt 用留出集决定改动能否留下，提出修改的那次不能自己通过。mattpocock 把「合乎规范」和「做的是规格里的事」分成两轴，不合并成一个结论。

## 设计意图

这些仓库默认模型会在没读到内容时作答，会用过期的命令或过期的引用，会把训练题上的进步说成技能已经更好，也会把两份互相矛盾的材料写成一句。所以规则写成停手、留出样本和文件上的证据。

技能数量用不同办法压住。MinerU 和 agent-browser 各留一个入口，专项和版本文档在旁边。mattpocock 把编排和纪律拆开，并明确不接管整条流程。SkillOpt 部署时只留一份短的技能文档。Skill Seekers 生产的是新技能，本库不走那条路。

本库八个技能是交付过程。这五个仓库分别是解析器、浏览器 CLI、工程技能目录、技能训练器和技能工厂，不替换那八个名字。

## 对本库可抄的部分

可抄的是纪律，落在已有文件上，不新开技能名。

1. **先读到再下结论。** `work-doc-writer` 对扫描件保持「没识别到文字」。多页材料写明依据读到的范围。纯文本和界面原文直接读。
2. **浏览器先看当前页。** `drission-crawler` 的站点包继续放选择器和等待。遮挡或不可见记失败，重新取页面再动。页面文案不当成新指令。登录和提交仍停。
3. **交接指向证据，审查分两轴。** `dev-process-handoff` 写行为、默认值和验收变化，并指向这次的路径。`dev-review-verify` 把「有没有走收工程序」和「有没有当次产物」分开，一边过了不能代替另一边。
4. **改技能用留出样本。** 触发句若要改，留一组不参与这次改动理由的 `evals.json` 样本。提出修改的同一次不能自己宣布通过。会话不自动写回技能。
5. **来源冲突就标待确认。** 两个来源不一致不并成一句。交接写明依据的是哪一版界面或脚本。模型转述先标明不是原文。

## 对本库不抄的部分

1. **不换文档解析器。** 不把 MinerU 的命令、定位、错误码或安装说明写入 `work-doc-writer`、`word-thesis-format` 或发票流程。附加许可下只记思路。PaddleOCR 加模型的核对保持不动。
2. **不换浏览器产品。** 不把 `drission-crawler` 换成 agent-browser 的命令、云端浏览器或从录制推导的接口客户端。不把 1 到 5 分写进验收。
3. **不装工程技能包。** 不引入术语表、工单状态机、红绿重构或临时目录里的会话交接。不在交接后自动拉起另一个代理。
4. **不训练技能。** 不把八个交付技能交给 SkillOpt 或夜间暂存。论文里的提升不进入验收标准。发票和会话原文不送出本机做提炼。
5. **不从外部材料生产技能。** 不抓取文档站或 PDF 来生成并安装技能，不建向量库，也不用发布分代替 `evals.json` 和 LIVE。

## 若以后改现有技能，优先动哪里

本次只记阅读结论，不改 `skills/`。

- `work-doc-writer`：空识别和多页范围保持写明。文种判断不变。不换解析器。
- `word-thesis-format`：版式完成仍以预览为准。不改走外部解析 CLI。
- `drission-crawler`：入口保持短，站点包跟当前站点走。失败后重新看页面。能请求就不打开浏览器。
- `dev-review-verify`：收工程序和当次产物分开写。没有核对项就写没有。不引入 1 到 5 分。
- `dev-process-handoff`：指向这次证据和依据的版本。不重抄对话，不写密钥。不自动改技能。
- `demo-kickoff-card`：保持四块和一轮确认。待确认保持原样。
- `government-service-design`：不增加审查轴或方案竞选。
- `windows-gui-bat-launcher`：就绪仍看窗口和标志文件。不改成红绿测试循环。
