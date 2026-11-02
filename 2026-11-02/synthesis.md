# 2026-11-02 综述

当日阅读 5 个仓库。星标为当日 GitHub API `stargazers_count`。Firecrawl 仓库根是 AGPL-3.0，抽查的构建技能 frontmatter 写 ISC，该篇只记思路。PaddleOCR 的代码推送停在 2026-09-16，星标仍高，笔记不把星标说成近期功能发布。

去重：已合入的 2026-10-26、2026-10-27，以及未合并的 2026-10-28、2026-10-29、2026-10-30 笔记里出现过的仓库，今天不重复。另看了 Stagehand 自带的 browse 技能，它和 2026-10-27 的 Browserbase 技能包是同一条浏览 CLI，不单写。Playwright MCP 仓库的使用说明把编码代理指到 CLI 技能；该 MCP 仓库里查到的 `SKILL.md` 是维护者无人值守分诊，所以浏览器篇写在 Playwright CLI。

| 笔记 | 仓库 | 星标 | 许可（查阅所见） | 类型 |
| --- | --- | --- | --- | --- |
| [docling.md](docling.md) | [docling-project/docling](https://github.com/docling-project/docling) | 70006 | MIT | 文档转换；使用技能与贡献者评审分开 |
| [paddleocr.md](paddleocr.md) | [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 92126 | Apache-2.0 | 官方两份 OCR 技能（云端 API） |
| [playwright-cli.md](playwright-cli.md) | [microsoft/playwright-cli](https://github.com/microsoft/playwright-cli) | 14872 | Apache-2.0 | 浏览器命令行技能，快照后操作 |
| [firecrawl.md](firecrawl.md) | [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 197839 | 仓库 AGPL-3.0；技能 frontmatter 写 ISC | 把网页数据接进应用的构建技能 |
| [ecc.md](ecc.md) | [affaan-m/ECC](https://github.com/affaan-m/ECC) | 295201 | MIT | 大型 harness；抽查评测、浏览器验收和学习钩子 |

## 写法上的共同点

五份材料都把「还不能下结论」写在成功旁边。Docling 要求报转换状态和页数，近空、重复和替换字符要改路。PaddleOCR 把没有内容列为错误，并禁止失败后改用模型视力。Playwright CLI 每步之后给当前快照，截图不是主证据。Firecrawl 把抓取成功和业务对象仍有效拆开，缓存要能看出来。ECC 在没有视觉基线时要求写无法下结论，不能静默通过。

第二处是入口先分流，细则跟着会变的东西走。Docling 用一张表把命令行、SDK、抽取、分块和远程服务分开，长文在 `references/`。PaddleOCR 用两份技能分开纯文字和版面。Playwright CLI 用 ref 做默认定位，大页面改查找或限深，会话和持久化配置不是默认。Firecrawl 按「有网址、只有查询、必须点击」升级。ECC 用安装预览限制一次放进上下文的技能数量，废弃技能在 description 第一句指向替代。

第三处是外部结果不当成指令或完成。页面快照、识别文本、缓存副本、评测工具的自测输出，都只是材料。Docling 的评审技能写明没跑的检查不能说成通过，有字也不证明结构对。ECC 写明工具测试通过不等于已经隔离或允许升级。

## 设计意图

这些仓库默认模型会概述没读到的 PDF，会用行识别去读表格，会沿用过期的页面引用，会把旧缓存说成刚刚打开，也会把试通一次说成可以收工。规则因此落在坏结果的样子、技能之间的负例、当次快照，以及连续成功和基线。

技能数量差得很大。Docling 把读文档和改仓库分成两层。PaddleOCR 只有两份。Playwright CLI 的使用技能是一份，另有维护者技能。Firecrawl 在本仓库只放构建技能，会话抓取指到别处。ECC 有三百多个技能目录，并用预览和按名安装来补救。本库仍是八个交付技能，不跟着套件的个数增长。

## 对本库可抄的部分

可抄的是纪律，落在已有文件上，不新开技能名。

1. **近空和乱码也要写明。** `work-doc-writer` 在空文本之外，把近空、大段重复、替换字符写成没识别到，并写页范围。纯文字和带表格的版面在说法上分开，再走现有本地核对。有字不等于表格已经还原。写进手册前看识别有没有被截成摘要。
2. **浏览器每步留下当次页面。** `drission-crawler` 成功操作后也把回读落到证据路径。页面大时先按目标文字取局部。定位对不上就重新取页。看不清点哪里就问人。能直接取到的仍不开浏览器；抓到或导出成功，还要回读业务字段是否仍有效。
3. **必需路径要连续过。** `dev-review-verify` 不把「重试几次有一次过」写成验收完成。没有上一版页面、上一份导出或书面预期时，写未验收，并写明缺的是基线。`evals.json` 的应触发和不应触发分开看。没跑的检查保持写成没跑。

## 对本库不抄的部分

1. **不换解析器和识别云。** 不把 Docling 或 PaddleOCR 官方 API、令牌、托管服务写进文档和发票链路。扫描件留在本机。本地 PaddleOCR 加模型核对保持不动。
2. **不换浏览器产品。** 不把 `drission-crawler` 换成 Playwright CLI、Firecrawl 或 ECC 的浏览器验收。不挂日常浏览器，不把登录和提交交给代理。
3. **不摘 Firecrawl 正文。** 仓库根是 AGPL，技能 frontmatter 的 ISC 不足以支持摘录。只保留上面的分流。
4. **不装 harness。** 不引入 ECC 的钩子、五轴自评分、SHIP 裁决或自动把会话写回技能。触发样本仍在 `evals.json`，真实产物仍走 LIVE。

## 若以后改现有技能，优先动哪里

本次只记阅读结论，不改 `skills/`。

- `work-doc-writer`：空文本、近空和乱码都写明，并带页范围。文字和版面不要混成一次识别。不换引擎，不送出扫描件。
- `word-thesis-format`：版式完成仍看预览。检查没跑就不写通过。
- `drission-crawler`：每步回读落文件；大页面先取局部；能请求就不打开浏览器。登录和提交仍停。
- `dev-review-verify`：必需路径连续过才写验收完成。缺基线写未验收。不引入分数和发布裁决。
- `demo-kickoff-card`：成功标准仍在动手前写在卡上，供后面的连续核对使用。
- `dev-process-handoff`：写明依据的是哪一次页面或导出。旧缓存和模型转述不写成当次事实。
- `government-service-design`：不增加视觉基线竞选或可访问性分数。看不清的控件问人。
- `windows-gui-bat-launcher`：就绪仍看窗口和标志文件。脚本或工具自测通过不等于窗口已经出现。
