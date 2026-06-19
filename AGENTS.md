# AI Agent 全栈 Roadmap 项目规则

## 仓库

内容型仓库，不是代码项目。核心产出是一份面向 Node.js / 前端开发者的 AI Agent 全栈开发 Roadmap。

## 文件

- `README.md` / `README.zh.md` — 门面（英/中）
- `ROADMAP.md` — **核心**，7 阶段完整内容（中文）
- `outline.md` — XMind 大纲，与 ROADMAP.md 结构同步
- `assets/` — roadmap.png / roadmap.xmind
- 中文版为主，改内容时 `outline.md` 和中英文 README 需同步

## 编辑规范

- 中文全角标点：，  。  、  ：  ；  （） 【】
- 中英文之间空格、中文与数字之间空格
- 专有名词按官方大小写：Claude Code、Vercel AI SDK、pgvector
- 内部链接用相对路径，外部用完整 HTTPS

## 内容原则

- **能力地图，不是工具排行榜** — 选最稳、最能说明概念的，不选最火的
- **面向有 Node.js/前端基础的人** — DB/Redis/OAuth/Docker 默认已掌握，聚焦 AI 增量
- **概念优先于产品** — 说"Agent 循环"，不只说"Claude Code 的 Agent Loop"
- **表述要稳** — 避免绝对化用语，不确定的不加
- **🟢 必学 / 🔵 工程贯穿 / 🟡 进阶选修** — 用标签帮读者取舍
- 不展开教程级内容，只说"学什么"和"为什么"

## 改动检查

1. 概念够不够稳定？
2. 放哪个阶段、哪个标签层级最合适？
3. 前后章节有无引用需要同步？
4. `outline.md` 和两个 README 是否同步更新？
