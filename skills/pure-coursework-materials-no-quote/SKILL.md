---
name: pure-coursework-materials-no-quote
description: Compile official university program/module assessment details into a client-ready coursework-only deliverable (no pricing, no quote). Use when given school/program/degree/year/scope to extract modules, workload, credits, semester, risks, and output a formatted single-sheet Excel.
---

# 纯课程资料整理技能（不含报价）

## Overview
Produce one client-ready output that includes:
- Coursework table (课程信息 + 作业量 + 风险)
- Formatted Excel in a single sheet
- No quote block, no pricing fields

## Required Inputs
- School (university)
- Program/Department
- Degree level (UG/PGT/PGR)
- Entry year / target academic year
- Scope: full year / semester / selected modules

Optional inputs:
- Module codes / module names (when partial scope)
- Current student year (background only)
- Target covered year/level (for module selection)
- User-provided course outlines/syllabi

## Workflow

### 0) Intake confirmation (mandatory before research)
Ask first and wait for confirmation if key inputs are missing.

Mandatory confirmation items:
- Data mode:
  - `A` 自行搜索官方来源整理
  - `B` 根据用户提供课程大纲整理
  - `C` 混合模式（官方+用户大纲）
- Coverage scope: full year / semester / selected modules.
- Elective selection finalized?
  - If yes: request module codes/names.
  - If no: confirm whether to use official sample pathway.
- Year/Level clarification:
  - 当前在读年级（仅背景信息）
  - 本次要做的目标年级/Level（用于选课，必填）
  - If conflict exists, always follow target year/level.
- Confirm phrase (use directly):
  - 你现在读哪个年级（仅背景）？
  - 这次要整理的是哪个年级/Level的课程（按这个出结果）？
  - 确认一下：例如学生2026年在读大二，你这次要我整理的是否就是2026学年大二这一年的课程？

Hard stop rule:
- Do not generate final output if missing info would materially change module set or workload totals.
- Stop when target covered year/level is ambiguous.

### 1) Find sources (mode-aware)
- Mode A: Use official university domains + official handbook/catalog/DRPS/module pages.
- Mode B: Use user-provided outlines as primary source; keep per-row source labels as `用户提供课程大纲` + filename/page if available.
- Mode C: Merge both; official source has priority for policy/credit/semester conflicts, and note reconciliation in 备注.
- Match entry year first.
- Record source year + URL (or uploaded-file reference) for key facts.
- Also check official academic calendar term dates for target year; include only when exact dates are available.

### 2) Build covered module list
- If full-year scope, extract full required module list.
- If partial scope, include only specified modules.
- Extract credits and semester/teaching period.

### 3) Extract assessment workload
- Split each module into assessment components (one row per component).
- Extract weight, word count, duration, pages, and task description.
- If workload details missing, estimate and mark in 备注.

### 4) Convert workload to words
Use fixed conversions:
- 1 hour exam ~= 1500 words
- 1 minute presentation ~= 100 words
- 1 page ~= 300 words

Write converted values in `字数/时长（含换算）` and explain conversion/estimation in `备注`.

Mandatory estimation rule:
- Every assessment row must have numeric word-equivalent.
- If duration unknown/not published, estimate by matching same-credit modules and using highest observed total workload in that credit band as reference.
- Keep total workload roughly aligned across same-credit modules unless official data indicates otherwise.

## Output format (client-facing)
Always include:

1. Basic info block
- 学校/专业/学位/入学年份
- 覆盖范围
- 专业概述
- 核心知识/技能/软件
- 学分要求
- 校历信息（目标学年学期起止时间）
  - If official dates found, show them.
  - If not found, omit this row.
- 重要提醒（如官方迟交处罚/缺考规则；若官方可得则展示）
- 信息源

2. Coursework table
- 序号 | 课程名称 | 学分 | 必修/选修 | 学期 | 作业 | 字数/时长（含换算） | 占比 | 作业简述 | 风险评估 | 判断依据 | 信息源 | 备注
- Sort: Semester 1 -> Semester 2 -> Full Year

作业简述 minimum content:
- Task objective (what to deliver)
- Expected output format (essay/report/slides/code/case)
- Whether special software/tools may be needed
- Important reminders (late penalties/strict rules) when available

3. Summary row
- 总字数（含估算）

## Excel deliverable (required)
Generate a `.xlsx` with a single sheet:
- Top: basic info block
- Middle: coursework table with styled header
- Bottom: total workload summary row

Formatting baseline:
- Header bold + light fill
- Practical column widths
- Wrap text on all content cells
- Keep info fields horizontal (label/value layout, merged value cells)
- `信息源` cells must be clickable hyperlinks (not plain text)

Template lock (default):
- Match style of `/Users/wangcaidi/Desktop/最强业务/qmul-business-management-year3-2025-selected-modules-quote-v1.xlsx`
- Keep one-sheet structure and visual style
- Remove quote section entirely

## Quality Guardrails
- Do not hallucinate missing official facts.
- Mark uncertain values clearly in `备注`.
- For partial scope, do not include uncovered modules.
- Keep source years explicit.
- Final pre-delivery checks:
  - every row has numeric word-equivalent
  - risk column has adjacent 判断依据
  - source links are clickable and year-labeled where available

## Strict exclusion
- Never output any pricing content.
- Never include quote/package/price rows.
- If user asks for price in this skill, respond: `当前为纯课程资料整理模式，不包含报价。`
