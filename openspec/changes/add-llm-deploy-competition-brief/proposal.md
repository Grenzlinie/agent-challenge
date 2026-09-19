# Proposal

## Why

比赛 B（LLM 部署赛）赛题已于 2026-09-18 20:00 在飞书群「DP-Arena内部赛」正式发布（开赛公告见群消息，赛题正文见邀请函 wiki）。本仓库作为团队单一事实来源，需要把赛题要点固化为规格，作为后续部署方案设计、迭代与提交物管理的基线。

## What Changes

- 新增比赛 B（LLM 部署赛）的赛题要点规格：任务目标、固定模型与硬件、评测方式、交付物、评分规则、赛期，内容全部来自官方赛题文档与群公告。
- 不涉及代码改动；本仓库为项目管理仓库。

## Capabilities

### New Capabilities

- `competition-b-llm-deploy`: 比赛 B「LLM 部署赛」的赛题要点与参赛约定——在固定模型（GLM-5.3-Flash 320B-A18B）与统一 A100 硬件额度下，通过部署配置优化把模型响应指标调到最好，覆盖评测方式、可优化范围、交付物与评分规则。

### Modified Capabilities

（无）

## Impact

- 影响范围仅限 `openspec/` 内的规格与变更目录，以及 README.md 的比赛表格备注。
- 算力依赖：arena 算力池加入申请已获批（trisol `team join-requests list` 状态 approved）。
- 赛题原文：https://dptechnology.feishu.cn/wiki/Pda8wY9NFiXS7xkN75qcESzXnvU ；比赛页面：https://play.bohrium.com/llm-arena/competitions/llm-deploy-arena-v1
