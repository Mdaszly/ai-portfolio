# 阿里云百炼原生 RAG Assistant

**技术栈**：阿里云百炼（Qwen-Max + text-embedding-v4 + qwen3-rerank）  
**应用类型**：Agent 应用（非 Workflow）  
**证据文件**：`rule-prompt.png` · `data-connector.png` · `knowledge-base-1.png` · `knowledge-base-2.png`

---

## 业务问题

需要快速搭建一个可配置的商场智能客服 RAG 系统，验证阿里云百炼平台原生 Agent 能力与知识库检索效果，作为 Dify Workflow 版本的对照实验。

---

## 方案决策

1. **规则与提示词工程**  
   设计「会员停车」「固定规则」「禁止推测」三类约束，通过系统提示词 + 变量注入实现知识库优先、禁止幻觉、转人工兜底的策略（见 `rule-prompt.png`）。

2. **数据连接器与工具**  
   接入科传文档库、searchFile、getFile 三个工具，实现结构化 FAQ、营业时间、楼层导览、会员等级等知识的检索与调用（见 `data-connector.png`）。

3. **知识库创建与索引设置**  
   采用「智能切分 + 600 字符最大分段长度」，搭配 text-embedding-v4 向量模型 + qwen3-rerank 重排序，实现问答模式下的语义检索与重排（见 `knowledge-base-1.png`、`knowledge-base-2.png`）。

4. **记忆与上下文控制**  
   开启短期记忆（10 轮上下文），支持多轮对话中的连贯追问，同时通过规则约束避免短期记忆导致的数字幻觉与品牌误判。

---

## 关键配置亮点

- **知识库优先 + 禁止推测**：提示词明确「仅依据知识库内容回答」「不得编造」「知识库没有的信息，明确回复『暂无该信息』」
- **品牌拒答模板**：对「优衣库」「海底捞」等未覆盖品牌，自动触发拒答 + 转人工流程
- **检索参数调优**：TopK=10、关键词 TopK=50，配合重排序模型提升相关性
- **成本可控**：使用标准版知识库（0.03 元/月）+ 按 Token 计费的 embedding 模型，适合中小规模验证

---

## 与 Dify Workflow 版本对比

| 维度 | 阿里云百炼原生 Agent | Dify Workflow |
|------|---------------------|---------------|
| 编排方式 | 平台内置 Agent 框架 | 自定义节点 + 循环反馈 |
| 知识库管理 | 平台托管切分/索引/重排 | 需手动配置 chunk 与 embedding |
| 提示词调试 | 可视化变量注入 | 代码级 Prompt 模板 |
| 喂养迭代 | 依赖平台日志与人工观察 | 25 条测试集 + 8 轮 Bad Case 回归 |
| 交付物 | 控制台截图 + 对话记录 | feeding-test-log.md + 完整 Workflow 图 |

本项目作为「平台级 RAG 快速验证」案例，证明在无需自建编排框架的情况下，同样能完成知识投喂、规则约束与多轮对话控制。

---

## 复现步骤

1. 进入阿里云百炼控制台 → 应用中心 → 创建 Agent 应用
2. 按 `rule-prompt.png` 配置系统提示词与变量
3. 按 `data-connector.png` 添加数据连接器与工具
4. 按 `knowledge-base-1.png`、`knowledge-base-2.png` 创建知识库并设置索引参数
5. 发布后在对话窗口测试「钻石会员停车」「优衣库在几楼」等边界用例

---

## 交付物

- 规则与提示词配置截图（rule-prompt.png）
- 数据连接器与工具配置截图（data-connector.png）
- 知识库创建与索引设置截图（knowledge-base-1.png、knowledge-base-2.png）
- 对话测试记录（控制台可导出）

**下一步**：将本项目与 Dify Workflow 版本的 Bad Case 进行对照，提取平台原生 Agent 的优势与局限，形成对比报告。