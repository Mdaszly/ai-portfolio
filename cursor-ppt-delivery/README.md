# Cursor 辅助 PPT/Word 快速交付案例

**技术栈**：Cursor + Kimi + TRAE（国产模型）  
**交付物**：每日工作进度汇报（Word）· 智能商场客服系统 PPT（12 页）  
**证据文件**：`daily-report-word.png` · `cursor-tool-selection.png` · `ppt-preview.png` · `challenge-solution.png`

---

## 业务场景

需要同时交付：
- 一份结构化的「每日工作进度汇报」（Word 格式）
- 一份 12 页的项目验收 PPT（封面、目录、项目背景、工作流、挑战与解决方案等）

时间紧、内容多，需要在保证质量的前提下控制 token 成本。

---

## 方案决策

1. **Cursor 负责前 4 页打样 + Word 文档**  
   使用 Cursor + Kimi 完成：
   - Word 格式的「每日工作进度汇报」（含基本信息、今日工作概述、Dify 工作流搭建详情、Cursor 工具选择表、遗留问题、下周计划）
   - PPT 前 4 页（封面、目录、项目背景、系统工作流架构）
   - 全局设计规范（配色、字体、圆角、页数等）

2. **TRAE 接力剩余 8 页，节省 token 成本**  
   把剩余页面（挑战与解决方案、项目总结等）的脚本和规范导出后，交给 TRAE（国产模型）继续生成，避免大 token 消耗。

3. **混合工具链成本优化**  
   - Cursor 负责「打样 + 结构化文档」（质量高、上下文连贯）
   - TRAE 负责「批量生成剩余页面」（成本低、速度快）
   - 最终人工整合，确保风格统一

---

## 关键证据

- `daily-report-word.png`：Cursor 生成的 Word 格式每日工作汇报，含表格、列表、AI 一键美化痕迹
- `cursor-tool-selection.png`：Cursor 工具选择详情表（Word、PowerPoint、PPT Agent、MCP 服务器）
- `ppt-preview.png`：PPT 幻灯片预览（封面 + 目录 + 项目背景 + 工作流）
- `challenge-solution.png`：挑战与解决方案页面（第 9-12 页），展示 token 成本控制后的交付成果

---

## 与 JD 匹配度

- **Cursor AI 编程效率**：需求拆解、代码生成、Code Review、Vibe Coding 贯穿 3 个项目，90% 代码 AI 生成，本人负责方案选型与最终验收
- **混合工具链成本优化**：在 token 敏感场景下，主动选择 Cursor（高质量打样）+ TRAE（低成本接力）的组合，体现工程化思维
- **项目交付优先**：输出可直接使用的 Word 文档和 PPT 脚本，符合「项目交付优先」原则

---

## 复现步骤

1. 用 Cursor 打开 Kimi，输入「把这个工作流做成 PPT 进行项目汇报」
2. Cursor 生成前 4 页脚本 + 全局设计规范（`ppt-script.png`、`design-spec.png`）
3. 把剩余 8 页脚本导出，交给 TRAE 继续生成
4. 最终在 PowerPoint 中整合，人工微调风格一致性

---

## 交付物

- Word 格式「每日工作进度汇报」（`daily-report-word.png`）
- 12 页 PPT 脚本 + 设计规范（`ppt-script.png`、`design-spec.png`）
- 完整 PPT 幻灯片预览（`ppt-preview.png`、`challenge-solution.png`）
- Cursor 工具选择与 MCP 配置记录（`cursor-tool-selection.png`）

**下一步**：把这个案例合并到简历的「AI 编程与 Cursor 工作流」模块，突出「混合模型成本优化 + 快速交付」能力。