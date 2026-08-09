先执行通用检查，再选择相关的论文类型，不要把所有检查项强加给每篇论文。

## 通用证据检查

- 确认准确的研究问题、作者声称的贡献、不解决的问题和基本假设。
- 区分作者声称的结论和实验真正能够证明的结论。
- 记录数据集来源、划分、过滤、污染风险、预处理和许可证。
- 记录 Baseline 版本、实现来源、调参预算、模型版本、Prompt、随机种子、重复运行次数和推理设置。
- 检查指标定义、方向、聚合方式、不确定性、Judge 配置，以及指标是否匹配论文声称的能力。
- 检查最强 Baseline、主结果表、最关键消融实验、失败分析、局限和附录。
- 方法改变算力、时延、Token、费用、标注或人工审核成本时，记录对应变化。
- 区分“论文提供了某项材料”和“已经检查或运行了某项材料”。

## 基础模型、模型架构或训练论文

追踪：

`数据 → 表示方式 → 模型架构 → 训练目标 → 优化过程 → 推理过程 → 评测`

检查：

- Tokenization、输入表示、上下文长度、参数规模和架构改动；
- 预训练、继续预训练、指令微调、偏好优化、蒸馏或推理时计算所处阶段；
- Loss 或 Reward 目标、采样方式、课程学习、正则化和优化预算；
- 训练数据组成、去重、泄漏控制和数据质量假设；
- Scaling 对比、同等算力 Baseline、推理预算和效率权衡；
- 分别隔离数据、架构、训练目标和算力的消融实验；
- 训练分布之外的泛化，以及负向或安全案例表现。

训练数据、参数量或推理预算同时改变且缺少控制实验时，不要把提升直接归因于模型架构。

## RAG、检索或知识系统论文

追踪：

`语料库 → 解析与清洗 → 切块与索引 → Query 变换 → 检索 → 重排 → 构建上下文 → 生成 → 引用与评测`

检查：

- 语料时效、使用权限、文档粒度、Metadata、Chunk 大小、重叠和索引版本；
- Embedding 模型、词法或稠密检索、混合融合、Top-k、Reranking、过滤和 Query Transformation；
- 检索上下文怎样排序、截断、标注来源并进入生成阶段；
- Gold Document、Reference Answer、无答案案例、冲突文档和对抗内容；
- Retrieval Recall 或命中率、Context Relevance、Faithfulness、Answer Correctness、引用准确性、时延和成本；
- Oracle Retrieval 和 No-Retrieval 对照，能否区分检索失败与生成失败；
- 语料库、评测问题和模型训练数据之间的泄漏。

没有索引和检索证据时，不要把网页搜索或长上下文 Prompt 称为“经典向量 RAG”。

## Agent、Workflow 或 Tool Use 论文

追踪：

`Task → Trial → State/Context → Model Decision → Action/Tool → Environment Update → Termination → Outcome → Grader`

检查：

- Task 定义、Environment、Observation、Action Space、Tool Contract、State、Memory、Planner 和控制循环；
- 路由、重试、最大步数、终止、超时、错误处理、权限和人工介入；
- Transcript 或 Trajectory 怎样保存，中间行为是否纳入评测；
- Simulator 行为、环境确定性、工具结果真实性和状态转移有效性；
- 单次成功与重复 Trial、`pass@k`、`pass^k`、方差、成本、时延和安全违规；
- Outcome Grader、确定性规则、LLM Judge、人工评价和 Judge 模型敏感性；
- 失败应归因于模型、Prompt、Tool Schema、工具实现、Context、Environment、Grader 还是基础设施。

没有部署证据时，不要从 Benchmark 成功率推断生产可靠性。

## Benchmark、数据集或评测论文

追踪：

`来源总体 → 采样与过滤 → Task/Case → Trial/Prediction → Evidence/Transcript → Grader → Metric/Aggregation → Report`

检查：

- Intended Construct：论文声称衡量的能力或质量到底是什么；
- Task 来源、纳入标准、标注流程、争议裁决、标注者一致性和版本管理；
- 训练、验证、测试集隔离，以及公开暴露、记忆、污染和 Benchmark 饱和风险；
- 环境配置、Fixture、Reference Answer、可执行测试、Simulator、Judge 和失败处理；
- 指标有效性、聚合方式、缺失或 Blocked Case、置信区间、重复 Trial 和显著性；
- Rule-based 和 Model-based Grader 的分工，以及 Judge Prompt、校准、偏差、泄漏和人类一致性；
- Benchmark 是适合模型排名、失败诊断，还是两者都支持；
- 数据集、Harness、依赖、模型端点和报告运行结果能否复现。

不要把排行榜分数当成完整的质量解释。必须恢复失败分类和诊断证据。

## 对齐、偏好优化或安全论文

追踪：

`行为或威胁模型 → 数据或反馈 → 目标或策略更新 → 评测 → 剩余风险`

检查：

- 威胁模型、攻击者能力、受保护资产、安全策略和预期部署边界；
- 反馈来源、标注指南、Preference Model、Constitution、Reward Signal 或合成数据流程；
- Helpfulness–Harmlessness 权衡、过度拒绝、Jailbreak 鲁棒性、分布偏移和自适应攻击；
- Benchmark 真实性、攻击多样性、Evaluator 独立性和训练数据向红队测试的泄漏；
- 涉及工具时的权限、Sandbox、Credential、Prompt Injection、数据外泄和 Blast Radius 控制；
- 剩余风险，以及缓解措施降低的是发生概率、影响范围，还是两者。

没有检查可用性和误拒绝时，不要把拒绝率直接解释为安全性。

## AI 系统、推理系统或框架论文

分别追踪：

- 控制面与数据面；
- 离线准备与在线服务；
- 请求主路径与后台维护路径；
- 稳态、过载、故障、恢复和升级行为。

检查：

- 组件边界、调度、Batching、Cache、State、持久化、一致性和 Backpressure；
- 硬件、模型、Workload、并发、序列长度、请求到达分布和 Benchmark 真实性；
- Throughput–Latency 权衡、百分位时延、长尾行为、内存、利用率、能耗和成本；
- 对比公平性、Warm-up、编译、缓存、量化、质量保持和故障恢复；
- 扩展上限、单点故障、运维复杂度和生产证据。

不要把 Microbenchmark 结论泛化到其硬件和 Workload 契约之外。

## 提取可复用知识

对每篇论文确认：

- **理解**：最值得记住的一项机制或评测思想；
- **实现**：能够动手构建的最小组件；
- **测试**：验证它所需的失败模式、数据集、Grader 和可观测性；
- **比较**：最接近的替代方案，以及各自占优的条件；
- **解释**：能够脱离原文、有证据支持地说明“问题—设计—结果—边界”；
- **扩展**：一项能够加深理解、形成学习证据的现实实验或项目改造。
