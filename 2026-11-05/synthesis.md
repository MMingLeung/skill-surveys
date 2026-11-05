# 2026-11-05 综述

当日阅读 5 个仓库。星标为当日 GitHub API `stargazers_count`。anydoc、Chrome DevTools、ego lite、SkillSpector 都有 `SKILL.md`。Agent Skills 规范仓库没有作为产品的技能目录，它定义 `SKILL.md` 和两套评测，因此保留。规范的代码为 Apache-2.0，文档为 CC-BY-4.0，该篇只转述并短引。SkillSpector 的坏样例没有打开。Cookie 读取、浏览器配置迁移和扫描规则都没有摘步骤。

同日看过但没有写成笔记的邻近仓库：`microsoft/markitdown`（193982 星，MIT，树上没有 `SKILL.md`）、`run-llama/liteparse`（12987 星，Apache-2.0，没有 `SKILL.md`）、`web-infra-dev/midscene`（15511 星，MIT，没有 `SKILL.md`）。办公文件这一篇用带技能的 anydoc。

去重：已合入的 2026-10-26、2026-10-27，以及未合并的 2026-10-28 至 2026-11-04 笔记里出现过的仓库，今天不重复。MinerU、Docling、PaddleOCR、Browser Use、Playwright CLI、agent-browser、Browserbase 技能包和 Firecrawl 主仓库都不在这一批。

| 笔记 | 仓库 | 星标 | 许可（查阅所见） | 类型 |
| --- | --- | --- | --- | --- |
| [agentskills.md](agentskills.md) | [agentskills/agentskills](https://github.com/agentskills/agentskills) | 26963 | 代码 Apache-2.0；文档 CC-BY-4.0 | 技能格式、触发评测与产物评测 |
| [anydoc.md](anydoc.md) | [firecrawl/anydoc](https://github.com/firecrawl/anydoc) | 23365 | MIT | 本机把办公文件转成 Markdown；扫描页需要另开 OCR |
| [chrome-devtools-mcp.md](chrome-devtools-mcp.md) | [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) | 54832 | Apache-2.0 | 浏览器调试技能：快照、截图、无障碍、排障 |
| [ego-lite.md](ego-lite.md) | [citrolabs/ego-lite](https://github.com/citrolabs/ego-lite) | 21750 | MIT；浏览器本体是独立下载 | 把已登录浏览器交给代理的技能存根 |
| [skillspector.md](skillspector.md) | [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | 24437 | Apache-2.0 | 安装前审查技能；坏样例未读 |

## 写法上的共同点

五份材料都把走错路写在走对路旁边。规范要求 description 同时写何时用，并用近邻任务当负例，而不是用毫不相干的句子充数。anydoc 把成功、转失败、用法错误、缺文字层分成四个退出码。Chrome 技能把瘦模式、只读模式和旗标拼错分成不同失败。ego 的清理说明要求先读范围，因为有的清理超出当前站点。SkillSpector 把目标技能当成不可信输入，扫描器不在就写不在。

第二处共同点是完成不看模型自己说，也不看一条没看对象的通过。规范要求通过带证据，空有标题算失败，两种跑法都会过的断言删掉。anydoc 的退出码 0 只表示转出了 Markdown。Chrome 要求读失败项，不拿分数代替；结构和截图是两种证据。ego 用结束标记判断帮助有没有被截断。SkillSpector 写明不要只靠分数，解释不了的高危不能因为仓库有名就降级。

第三处是入口短、细则跟着会变的东西走。规范建议正文少于 500 行，引用只往下走一层。anydoc 的技能就是一条命令和六条规则。Chrome 把命令表放在 CLI 技能里，并要求工具升级后重装技能。ego 的正文只要求去读当次 `ego-browser skill` 的输出。SkillSpector 不把整份扫描结果贴进报告。

第四处是外部文字和外部会话不当成可以继续执行的指令。规范把演示校验器标成不能用于生产。anydoc 的托管 OCR 要显式打开，而且整份文件离开本机。Chrome 的首页写明浏览器内容会进入代理，统计默认开着。ego 的登录态留在本机配置里，代理能直接用。SkillSpector 不许运行目标技能的脚本，也不许悄悄另开计费的模型审查。

## 设计意图

这些仓库默认模型会把空文本说成文件是空的，会用过期的元素编号继续点，会把截断的帮助尾巴当成全文，也会把星标或分数当成可以安装。所以规则写成退出码、重取快照、结束标记，以及没跑就要写明的审查。

技能数量仍然被压住。规范仓库自己不提供产品技能。anydoc 和 ego、SkillSpector 各一份入口。Chrome 用七份 description 把操作、无障碍、Cookie 和排障分开，避免一份技能什么都包。本库仍是八个交付技能，不跟着调试工具的个数增长。

本库八个技能是交付过程。这五个仓库分别是格式规范、文档转换器、浏览器调试通道、已登录浏览器和技能扫描器，不替换那八个名字。

## 对本库可抄的部分

可抄的是纪律，落在已有文件上，不新开技能名。

1. **触发句写清不负责什么，负例用近邻任务。** `evals.json` 继续用使用人会说的话。完全无关的句子留着也测不出抢触发。模型本来就会的泛泛步骤，不另开技能。
2. **读文件要分清失败种类。** 转失败、用法错误、没有文字层不是同一句「读完了」。扫描件写成没识别到。大文件落盘再读需要的部分。会把整份文件送出本机的步骤先问人。
3. **页面先等、再定位、再动作。** 这一次对不上就重新看。结构和截图都要有。只抽出文字，或只拿到没打开的报告，不算看过。
4. **长输出读完，没跑的检查写明没跑。** 帮助被截断就整份存下来。旗标或版本对不上就停。交接写下工具版本和跳过的范围。
5. **外部技能先看 description 和正文是不是同一件事。** 触发宽到会抢走其他任务，或脚本超出说明，就不采用。许可限制的正文只记思路。

## 对本库不抄的部分

1. **不装自动评测循环。** 不引入二十条查询、重复运行、令牌账本和自动改写 description。`skills-ref` 的格式校验不代替 LIVE。
2. **不换文书引擎。** 不安装 anydoc，不把 Word 交付改成 Markdown，不用托管 OCR。版式仍以本机预览为准。
3. **不换浏览器，也不继承登录态。** 不安装 Chrome 调试通道或 ego lite。不迁移 Cookie。登录、验证码和提交仍交给使用人。
4. **不把调试分数写进政务界面。** 无障碍分数、首屏指标和点击热区不进入 `government-service-design`。颜色和间距维持现有规范。
5. **不装技能扫描器。** 不运行坏样例，不用 0 到 100 分收工。静态扫描不能代替当次页面或文件。

## 若以后改现有技能，优先动哪里

本次只记阅读结论，不改 `skills/`。

- `dev-review-verify`：当次页面、导出文件或窗口仍是完成条件。退出码、转换成功和检查分数都不单独通过。必需检查没跑就写未验收完成。
- `work-doc-writer`：没有文字层写成没识别到。未知事实保持待确认。大附件落盘再摘。不接会上传整份文件的 OCR。
- `word-thesis-format`：版式完成仍以本机预览为准。Markdown 不代替 Word。
- `drission-crawler`：能请求就不打开浏览器。定位失败就重新看页面，一次只改一个原因。登录和提交交给使用人。不继承浏览器配置。
- `dev-process-handoff`：写下查了什么、跳过什么、工具或站点包版本。外部技能没装就写没装。
- `demo-kickoff-card`：保持四块。不另加评测工作区或审查报告模板。
- `government-service-design`：图标按钮仍要有能读的名字。不换成无障碍评分或落地页规范。
- `windows-gui-bat-launcher`：就绪仍看窗口和标志文件。不改成浏览器产品或调试通道的启动方式。
- `evals.json`：负例尽量写成近邻任务。不把外部基准、扫描分数和触发率实验写进样本。
