# AI Berkshire — 项目指令

## 项目概述

基于 Claude Code 的价值投资研究 Skill 合集。四大师框架：巴菲特、芒格、段永平、李录。
GitHub: xbtlin/ai-berkshire

本仓库包含投资研究工作流、研究报告和共用的校验工具。保持对 Claude Code 和 Codex 用户的兼容。

## 项目结构

```
skills/          — 投研 Skill 定义（.md），复制到 ~/.claude/commands/ 使用
tools/           — 辅助工具（financial_rigor.py 精确计算、twstock_data.py 台股FinMind取数）
reports/         — 投资研究报告输出
assets/          — 图片等静态资源
```

- `skills/*.md`：Claude Code 斜杠命令源文件。
- `codex-skills/*/SKILL.md`：Codex skill 包。大多数由 `skills/*.md` 生成；允许 Codex 专属的手写包，前提是明确标注，且不存在同名的 `skills/*.md` 源文件。
- `codex-prompts/*.md`：生成的 Codex 自定义 prompt，提供斜杠命令式的入口。这是兼容层；仍以 skill 为首选。
- `tools/*.py`：两套系统共用的财务校验与数据工具。
- `reports/`：研究输出。修改工具或 skill 时，不要改写无关的报告。
- `scripts/sync-codex-skills.py`：根据 `skills/*.md` 重新生成 Codex skill。
- `scripts/install-codex-skills.sh` / `scripts/install-codex-skills.bat`：
  在本地安装 Codex skill。
- `scripts/install-codex-prompts.sh` / `scripts/install-codex-prompts.bat`：
  在本地安装生成的 Codex 斜杠 prompt。
- `scripts/install-claude-commands.sh` / `scripts/install-claude-commands.bat`：
  在本地安装 Claude Code 命令。

## Claude Code / Codex 兼容规则

- 以 `skills/*.md` 作为工作流的权威源。
- 修改 `skills/` 中的任何文件后，运行：
  `python3 scripts/sync-codex-skills.py`
- 如果需要斜杠 prompt 兼容，再运行：
  `python3 scripts/sync-codex-prompts.py`
- 不要手动编辑生成的 `codex-skills/*/SKILL.md`，除非同时更新 `skills/` 中对应的源文件。
- 对 `codex-skills/` 下 Codex 专属的手写包，保持其明确标注为 Codex 专属；除非有意让 Claude Code 也采用该工作流，否则不要创建同名的 `skills/*.md` 文件。
- 工具路径保持与文档约定的克隆路径兼容：
  `~/ai-berkshire/tools/...`
- 共享规范只写在 `AGENTS.md`；`CLAUDE.md` 只做 `@AGENTS.md` 导入，不在其中新增规则。

## 报告目录结构

所有报告按**公司名**建文件夹，公司相关的所有报告放在对应文件夹内：

```
reports/
├── AI产业研究/              — AI产业链全景研究（置顶）
│   ├── AI五层蛋糕-产业全景研究-20260605.md
│   └── AI五层蛋糕-公众号-20260605.md
├── 腾讯/                    — 腾讯所有研究报告
│   ├── 腾讯-research-20260408.md
│   ├── 腾讯-earnings-2025Q4.md
│   ├── 腾讯-management-20260409.md
│   └── 腾讯-thesis.md
├── 拼多多/                  — 拼多多所有研究报告
├── 泡泡玛特/                — 泡泡玛特所有研究报告
├── 核电-industry-20260409.md — 行业报告放根目录
├── AI算力-funnel-20260509.md  — 漏斗筛选报告放根目录
├── AI-轮动判断-20260509.md    — 主题级综合判断报告放根目录
├── portfolio-latest.md       — 组合报告放根目录
└── 多公司对比-checklist-20260408.md — 多公司报告放根目录
```

## 报告命名规范

| Skill | 文件命名格式 | 示例 |
|------|---------|------|
| /investment-team | `{公司名}/` 目录内含4个视角+最终报告 | `reports/拼多多/最终报告.md` |
| /investment-research | `{公司名}-research-{YYYYMMDD}.md` | `reports/腾讯/腾讯-research-20260408.md` |
| /investment-checklist | `{公司名}-checklist-{YYYYMMDD}.md` | `reports/腾讯/腾讯-checklist-20260408.md` |
| /industry-research | `{行业名}-industry-{YYYYMMDD}.md`（根目录） | `reports/核电-industry-20260409.md` |
| /industry-funnel | `{行业名}-funnel-{YYYYMMDD}.md`（根目录） | `reports/AI算力-funnel-20260509.md` |
| /private-company-research | `{公司名}-private-{YYYYMMDD}.md` | `reports/字节跳动/字节跳动-private-20260408.md` |
| /earnings-review | `{公司名}-earnings-{期间}.md` | `reports/腾讯/腾讯-earnings-2025Q4.md` |
| /earnings-team | `{公司名}/` 目录内含4个大师视角+研究底稿+公众号文章+读者评审 | `reports/腾讯/腾讯-earnings-2025Q4.md`（公众号定稿） |
| /thesis-tracker | `{公司名}-thesis.md`（长期维护） | `reports/腾讯/腾讯-thesis.md` |
| /portfolio-review | `portfolio-latest.md`（根目录，持续更新） | `reports/portfolio-latest.md` |
| /management-deep-dive | `{公司名}-management-{YYYYMMDD}.md` | `reports/腾讯/腾讯-management-20260409.md` |

## /investment-team 文件结构

```
reports/{公司名}/
├── README.md                         — 研究框架概览+核心结论
├── 01-商业模式分析-段永平视角.md
├── 02-财务估值分析-巴菲特视角.md
├── 03-行业竞争分析-芒格视角.md
├── 04-风险管理层评估-李录视角.md
└── 最终报告.md                       — Team Lead 综合报告
```

## 投研分析核心原则（最高优先级）

- **客观、客观、客观**——所有投研分析必须基于事实和数据，严禁主观臆断
- 严格区分"事实"与"观点"：事实用数据支撑，观点必须明确标注为"观点"或"推测"
- **不预设立场**：不预设看多或看空，先摆数据、再推逻辑、最后得结论。结论必须从数据中自然推出
- 禁止使用"我认为"、"我觉得"、"显然"等主观表述，改用"数据显示"、"证据表明"、"根据XX来源"
- **呈现正反两面**：每个核心判断都必须附带反面论据（"但另一方面..."），让读者自己权衡
- 对不确定的事情诚实说"不确定"或"数据不足"，不要用推测填充确定性
- 明确标注低置信度结论、不完整数据和来源缺口。
- 所有skill（investment-team、investment-research、earnings-review等）在执行时都必须遵守以上原则
- 开始任何研究之前，先运行 `date` 命令确认今天的日期。以该日期作为“最新”数据（股价、市值、最近一期财报）的基准，并在报告开头写明数据截止日期。不要根据训练数据推断当前日期。
- 在把生成的研究视为可发布之前，使用报告审计工具：
  `python3 tools/report_audit.py ...`
- 本项目用于学习和研究，不构成投资建议。

## 报告语言与风格

- 所有报告使用**中文**
- 风格：直接、犀利、不说废话
- 数据必须标注来源，关键数据至少2个来源交叉验证
- 当 skill 要求校验时，财务数据必须来自至少两个独立来源。
- 估计值必须注明"估计"
- 评分使用★符号（★1-5），不含半星
- 穿插巴菲特/芒格/段永平/李录的语录点评

## 编辑规则

- 除非任务明确要求修改，否则保留现有的报告文件。
- 改动只限于所要求的 skill、工具、脚本或文档。
- 完成 skill/工具改动之前，运行相应的语法检查或生成检查。兼容性改动运行：
  `python3 scripts/sync-codex-skills.py`
- 要验证生成的 Codex 产物是否最新、且不改写文件，运行：
  `python3 scripts/sync-codex-skills.py --check`
  涉及斜杠 prompt 时，再运行：
  `python3 scripts/sync-codex-prompts.py --check`

## GitHub 操作

- 本地克隆路径：`~/ai-berkshire/`
- 远程仓库：`https://github.com/xbtlin/ai-berkshire.git`
- 推送前先 `git pull --rebase origin main`（远程经常有新提交）
- commit message 用中文，描述清楚改了什么
- 不要推送中间过程文件（如 data_collection.md），只推最终报告

## 常用命令

```bash
# 推送报告到GitHub
cd ~/ai-berkshire
python3 tools/reports_index.py          # 先刷新研究索引（必做）
git add reports/xxx.md reports/README.md reports/index.json README.md
git commit -m "添加xxx报告"
git pull --rebase origin main
git push origin main
```

```bash
# 只检查索引是否过期，不写盘（CI 也跑这条）
python3 tools/reports_index.py --check
```

## 注意事项

- 市值必须手算校验：股价 × 总股本，与报告市值对比
- 货币单位要明确（港币/人民币/美元/新台币），防止混淆
- PE/ROE等指标用 tools/financial_rigor.py 精确计算
- 市值、估值、跨来源核对和情景分析，使用精确计算工具：
  `python3 tools/financial_rigor.py ...`
- 台股数据用 tools/twstock_data.py（FinMind）获取，并按 skills/financial-data.md 台股章节交叉验证
- 报告写完后主动询问是否推送到GitHub
- **推送前必须跑 `python3 tools/reports_index.py` 刷新索引**，否则 CI 的索引校验会失败
- 新报告文件名带 `-YYYYMMDD` 后缀、正文首行写 `# 标题`，索引即可自动识别；
  需要覆盖时在文件头加 YAML front-matter（`title` / `date` / `type`），
  规范见 `reports/_index/README.md`
- 新建的**专题目录或筛选池目录**要登记进 `reports/_index/config.json`，否则会被当成公司
