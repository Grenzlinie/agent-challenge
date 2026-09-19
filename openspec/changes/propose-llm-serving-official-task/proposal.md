# Proposal

## Why

群主沈文博于 2026-09-18 20:00 发布开赛指南，指南内图片指向正式任务书。现有 `add-llm-deploy-competition-brief` 基于邀请函，未覆盖正式赛制且部分口径已不适用，需要以实际下载的任务书校正团队参赛依据。

## What Changes

- 提出「推理服务评测赛」正式任务规格，覆盖8×A100 固定模型部署、能力门槛、隐藏会话回放、N@SLO/TPOT 排名与服务接口。
- 更新 README 比赛表格，并保留邀请函与正式任务书之间的差异说明。
- 本提案建议替代 `add-llm-deploy-competition-brief` 的待审规格；旧提案保留为历史，不应将两套冲突口径同时归档为有效规范。
- 记录已知时间节点与尚未公布的截止时间；不把其他成员的审批记录视为本账号状态。

## Capabilities

### New Capabilities

- `competition-b-llm-deploy`：8×A100 固定模型部署、能力门槛、隐藏会话回放、N@SLO/TPOT 排名与服务接口。沿用现有待审提案的 capability 路径；当前 `openspec/specs/` 无已定稿规格，因此使用 ADDED。

### Modified Capabilities

无已定稿 capability。

## Impact

仅影响管理仓库的规格与 README。实现另建独立代码仓库；本变更不运行比赛、不占用算力、不提交竞赛答案。依赖官方 Playground 题面、Bohr/Wenyon 资源及相应算力权限；审批状态必须由当前账号 CLI 查询。
