# Spec Delta

## Purpose

以群内开赛指南所指向的正式任务书为依据，为团队提供可核验的输入输出、约束、评分与交付契约，纠正邀请函阶段的过时摘要，支撑后续独立代码仓库实现、测试和团队审查。

## ADDED Requirements

### Requirement: 固定资源和输入

服务 SHALL 部署固定 GLM-5.3-Flash（320B-A18B）于 8×A100-SXM4-80GB；自测使用 arena team、w1 集群。模型权重与任务语义冻结。输入包括能力评测请求与预渲染、输出长度冻结的多轮 Agent 会话；公开开发集用于自测，正式会话负载隐藏，内容与规模不公开。

#### Scenario: 区分开发与正式评测
- **WHEN** 团队准备性能评测
- **THEN** 不得把邀请函的完全可见 query 口径当作正式隐藏负载已公开

### Requirement: 服务协议

服务 MUST 提供 OpenAI 兼容 chat/completions（最终答案在 choices[0].message.content）、就绪 models 返回 200、引擎根路径 POST /generate（SGLang 形 SSE）及 POST /flush_cache。generate MUST 原样使用已渲染 prompt，不重复套模板，ignore_eos 生效并恰好产生 max_new_tokens；meta_info 如实上报 completion_tokens、prompt_tokens、cached_tokens。flush_cache 真正清除前缀 KV 并返回 2xx 与 success:true。服务须覆盖可能超过 10 小时的评测窗口。

#### Scenario: 切换并发档
- **WHEN** 平台请求清缓存后开展下一档测量
- **THEN** 前缀 KV 被实际清空；失败时该档不得被标为有效

### Requirement: 能力与压测门禁

aime26.points 与 gpqa-diamond.points MUST 均严格大于 95 才进入压测。有效档位 SHALL 满足 coverage=100%、harness_data=0、harness_render=0、engine_error<1%、infra_error<1%、四道 TTFT 门、各受控桶有样本、tpot_p95≤0.10 秒/token。四桶目标为 fast_intra 3s、overall_intra 5s、turn_start 15s、chain_start 30s；判定使用超标率的95%单侧下界高于5%才失败的统计余量，不是自行固定放宽阈值。

#### Scenario: 能力分等于门槛
- **WHEN** 任一科 points 为 95
- **THEN** 不进入压测，不得宣称已通过能力门槛

### Requirement: 顺位排名

平台 SHALL 从 N=10 起在 2/6/10/14/18/…（步长4、无上界）爬坡，取实测全部门禁通过的最大 N 为 n_at_slo。排名先比 n_at_slo 越大越好，再比该有效档 tpot_mean 越小越好；两项不加权合成。TPM 仅报告不排名；连 N=2 都失败时 n_at_slo=null，排在有有效 N 的提交之后。

#### Scenario: 容量相同
- **WHEN** 两份提交 n_at_slo 相同
- **THEN** 比较该档 tpot_mean，而非 tpot_p95 或 TPM

### Requirement: 唯一提交契约

正式产物 SHALL 为 /app/submission/submission.json，image 与 command 为必填非空字符串，env（字符串映射）和 model_name（默认 default）可选。镜像须为授权的 LBG 打包镜像，建议固定 digest；不得提交 base_url、api_key、密文、公网端点或 team/cluster。镜像可拉取、服务就绪与接口在计分时核验。Playground 提交另附真实会话轨迹。

#### Scenario: 提交审查
- **WHEN** 团队准备提交配置
- **THEN** 校验四字段契约和实际镜像接口；不把配置格式通过等同有效成绩

### Requirement: 质量与诚信约束

服务 MUST NOT 关闭 thinking、压低输出预算、截断历史、删 tools 换性能，伪造时间戳/token/缓存计数或假清缓存，不得还原隐藏题目、攻击或干扰评测及其他参赛者。赛后复核违规取消该提交全部成绩。

#### Scenario: 核查缓存优化
- **WHEN** 方案声称通过缓存改善 TTFT
- **THEN** 实际缓存命中和清理行为可被复核，上报与真实执行一致

### Requirement: 时间与资源边界

参赛记录 SHALL 标明开赛时间为 2026-09-18 20:00（Asia/Shanghai），所读公告与正式任务书未给出确定截止时间，不得自行填写。比赛算力仅用于比赛任务；凭据不得进入仓库或提交物。当前账号审批必须通过 CLI 独立核验，不复用其他成员的状态。

#### Scenario: 核对赛程与权限
- **WHEN** 团队准备启动比赛任务
- **THEN** 先核验本账号资源权限；截止时间记为待组织方公告
