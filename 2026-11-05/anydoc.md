# anydoc（办公文件到 Markdown）

查阅日：2026-11-05。

## 1. 来源

- 仓库：<https://github.com/firecrawl/anydoc>
- 默认分支是 `main`。查阅以 `main` 为准，最近推送 2026-10-23。
- 星标：23365（当日 GitHub API `stargazers_count`）
- 许可：MIT（仓库 SPDX、README 徽章、技能 frontmatter 的 `license: MIT`）
- 技能只有一份：`skills/convert-documents-to-markdown/SKILL.md`。本篇短引来自该文件。同组织的 [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) 已在 2026-11-02 记过，且仓库为 AGPL-3.0；本篇不使用那个仓库的正文。

## 2. 它是什么

anydoc 是一个 Rust 转换器，把 Word、PowerPoint、Excel、OpenDocument、RTF、EPUB、CSV 和带文字层的 PDF 收成同一套 GitHub 风格 Markdown。Node、Python 和浏览器里的 WebAssembly 绑定同一套转换。技能教代理调用 CLI：能在本机转完的文件不离开机器。

它不做 OCR。扫描页或纯图片页以退出码 3 结束。技能写明这时可以改跑 `--ocr hosted`，把整份文件送到 Firecrawl Parse。README 写明没有按页选择，需要 OCR 时整份都出去。Rust 库没有这个开关，也不会自己联网。

README 自述在 100 份文档上和另外六个转换器比过，语料不在仓库里。本篇不把那张分数表当成当日复测。

## 3. 写法特点

- description 写输入类型，并写「文件不能直接读的时候才用」。没有写何时不要送出本机。停手条件在正文的退出码里，不在 frontmatter。
- 正文很短，主要是一条命令和六条规则。支持的扩展名列在技能里，不让代理凭记忆猜。
- 格式从文件内容判断。只有检测行不通时才传 `--format`：例如从标准输入读 CSV，或扩展名缺失、错误。技能把退出码分成四档：`0` 成功，`1` 文档转不成，`2` 用法错误，`3` PDF 有页需要 OCR。原文是 “0 success, 1 the document could not be converted, 2 usage error, 3 pages of a PDF need OCR.”（`skills/convert-documents-to-markdown/SKILL.md`，MIT）。失败在标准错误打一行，CLI 不提问。
- 大文档用 `-o` 落成文件，再读需要的部分，不把整份流进上下文。
- 已经在 Node、Python 或 Rust 工程里时，技能要求用库，不要再套一层 shell。
- README 的功能表写：图片在 Markdown 里变成替代文本，原始字节留在文档模型上。抽查 README 的一处 Node 示例少了一个右括号，技能正文写的是 CLI。说明和邻近示例会分开走样。

## 4. 原理与设计意图

代理会把读到的空字符串说成「这份文件没有内容」，也会把退出码 0 说成版式已经可用。所以转换把「转不成」「用法错了」「缺 OCR」分成三个码。扫描页不是空文档，是没识别到文字层。

托管 OCR 做成显式开关，是因为默认同步出去会把发票、合同和内部材料送走。整份上传、不能按页挑选，是这条开关的代价，必须在调用前知道。

统一 Markdown 是为了让不同办公格式进模型时结构一致。它不保留 Word 的页、页眉和学校规定的字体。图片只剩替代文本时，操作手册需要的截图也不在这份输出里。

## 5. 对照本库

本库的文书是 `work-doc-writer` 和 `word-thesis-format`：对照源码写 Word，版式以本机预览为准。扫描件空文本要写成没识别到。anydoc 是另一个转换器。

### 可借鉴

- 读办公文件时把结果分成：转出来了、文件坏了或加密、命令用错、没有文字层。没有文字层就写没识别到，不写成空白正文。
- 大文件先落盘，再读要用的章节。不把整份合同或报表灌进对话。
- 扩展名和内容不一致时，以内容识别为准；识别不了就停下来问，不猜一种格式硬转。
- 会把整份文件送出本机的步骤，调用前要人确认。发票、监管材料和内部文档默认不走托管 OCR。
- 工具说明和旁边示例不一致时，以当次 `--help` 或技能正文为准，不沿用看着眼熟的旧片段。

### 不要照搬

- 不安装 anydoc，不把 `convert-documents-to-markdown` 写进本库，也不把交付 Word 改成 Markdown。
- 不用它的托管 OCR。退出码 3 在本库是「没识别到」，不是自动改跑云端。
- 不把 README 里的对比分数写进 `evals.json` 或收工标准。
- 不把只剩替代文本的图片当成操作手册的截图。`work-doc-writer` 仍用当次截图。
- 不把转换成功当成版式完成。`word-thesis-format` 仍以本机打开的预览为准。

## 6. 一句话建议

办公文件先在本机读文字，扫描页写成没识别到，大文件落盘再读；不把 anydoc 或它的整份上传 OCR 接进文书技能。
