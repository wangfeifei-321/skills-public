# skills-public

公共可用技能仓库。

## Skills
- skills/pure-coursework-materials-no-quote
- skills/dp-product-new-customer-quote

## 安装话术（复制到 Codex）
请使用 skill-installer，帮我从 GitHub 安装以下技能：
repo: wangfeifei-321/skills-public
paths:
- skills/pure-coursework-materials-no-quote
- skills/dp-product-new-customer-quote
安装完成后告诉我结果。

## 使用前置（dp-product-new-customer-quote）
为了输出最终报价数字（不仅是课程表），请在运行环境配置：
- `QUOTE_API_BASE`（私有报价 API 地址）
- `QUOTE_API_KEY`（私有密钥）
- Python `.xlsx` 写入依赖（推荐 `openpyxl`）。若缺失可执行：
  - `python3 -m pip install openpyxl`
