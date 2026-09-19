# Proposal

> 历史邀请函摘要：正式任务口径见 [替代提案](../propose-dpa-md-official-task/proposal.md)，待团队 review。本文审批陈述不代表其他账号的实时状态；请勿与替代提案同时归档为有效规格。

## Why

比赛 A（DPA部署赛）赛题已于 2026-09-18 20:00 在飞书群「DP-Arena内部赛」正式发布（开赛公告见群消息，赛题正文见邀请函 wiki）。本仓库作为团队单一事实来源，需要把赛题要点固化为规格，作为后续参赛方案设计、任务拆分与提交物管理的基线。

## What Changes

- 新增比赛 A（DPA部署赛）的赛题要点规格：任务目标、输入/输出与交付物、约束条件、评分规则、时间节点，内容全部来自官方赛题文档与群公告。
- 不涉及代码改动；本仓库为项目管理仓库。

## Capabilities

### New Capabilities

- `competition-a-dpa-deploy`: 比赛 A「DPA部署赛」的赛题要点与参赛约定——在结果正确的前提下优化 DPA4C 模型在单张 PPU 上的完整推理速度，覆盖任务目标、可优化范围、参赛流程、交付物与评分规则。

### Modified Capabilities

（无）

## Impact

- 影响范围仅限 `openspec/` 内的规格与变更目录，以及 README.md 的比赛表格备注。
- 算力依赖：arena team 加入申请已于 2026-09-18 获批（trisol `team join-requests list` 状态 approved），参赛流程可正常推进。
- 赛题原文：https://dptechnology.feishu.cn/wiki/N9STwPrFEiDLXbkSGZxcp4mFn2e ；比赛页面：https://play.bohrium.com/competitions/dpa
