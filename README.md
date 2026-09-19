# Agent 挑战赛 · 项目管理仓库

本仓库是参加两项比赛的项目管理仓库，使用 [OpenSpec](https://github.com/Fission-AI/OpenSpec) 做规格驱动的变更管理。

## 比赛

> 题目已于 2026-09-18 20:00 在飞书群「DP-Arena内部赛」发布，要点见下表备注与 `openspec/changes/` 下的对应变更。

| 比赛 | 链接 | 备注 |
|---|---|---|
| 比赛 A（DPA部署赛） | https://dptechnology.feishu.cn/wiki/N9STwPrFEiDLXbkSGZxcp4mFn2e | 同一 DPA4C 模型、固定 1024 原子周期体系、单张 PPU，方向为 CUDA 算子迁移与优化；结果正确前提下比完整推理速度；交付源码 patch + 测试结果 + 改动说明 + 复现镜像；比赛页面 https://play.bohrium.com/competitions/dpa |
| 比赛 B（LLM 部署赛） | https://dptechnology.feishu.cn/wiki/Pda8wY9NFiXS7xkN75qcESzXnvU | 固定 GLM-5.3-Flash（320B-A18B）MoE 模型与统一 A100 卡额度，优化部署配置提升模型响应指标；评测题为可见的真实线上 query；交付服务镜像 + 启动/运行配置；比赛页面 https://play.bohrium.com/llm-arena/competitions/llm-deploy-arena-v1 |
| 参赛指南 | https://dptechnology.feishu.cn/wiki/NevpwcEEGi2deek51TMcNTvDnAh | 注册 / Token / 赛道入口 |

**评分与轨迹规则**（不看轨迹、自由 Agent 架构、trace 文件上传绕限等）见 [docs/比赛规则说明.md](docs/比赛规则说明.md)。

## 仓库边界

本仓库是 **store 仓库**，只负责对齐需求与记录事实：比赛题目解读、方案规格、分工与进度。比赛代码**不放在这里**。

- 每个比赛项目另开独立代码仓库（多个项目则一题一仓），代码仓库只放实现
- 代码仓库需要读规格时，clone 本仓库并注册为 store：`openspec store register <path> --id agent-challenge --yes`
- 各项目代码仓库统一登记在下表，避免实现散落后找不到归属：

| 项目 | 代码仓库 | 备注 |
|---|---|---|
| 比赛 A | 待创建 | |
| 比赛 B | 待创建 | |

## 工具链约定

| 用途 | 工具 |
|---|---|
| 规格 / 变更管理 | `openspec`（本仓库） |
| Bohrium 资源（文件 / 数据集 / 任务 / 节点等） | `bohr` CLI |
| 数据集下载 | `wenyon`（`wenyon-cli`） |
| 算力资源 / Arena Team | `trisol`（team 待管理员审批） |

## OpenSpec 安装（新成员必读）

要求 **Node.js ≥ 20.19.0**（`node --version` 确认）。

```bash
# 1. 安装 CLI
npm install -g @fission-ai/openspec@latest

# 2. 验证
openspec --version   # 应输出 1.13.0 或更高

# 3. 克隆本仓库后，注册为本机 store
git clone git@github.com:Grenzlinie/agent-challenge.git
cd agent-challenge
openspec store register . --id agent-challenge --yes

# 4. 检查（输出 Issues: none 即成功）
openspec store doctor agent-challenge
```

常见问题：

- `openspec: command not found` → npm 全局 bin 不在 PATH：运行 `npm prefix -g`，把输出路径下的 `bin` 子目录加入 shell 的 PATH
- **不要**在本仓库运行 `openspec init`——`openspec/` 目录已初始化并配置好团队约定

## OpenSpec 使用

- 规格与变更：`openspec/`（`specs/` 为已定稿规格，`changes/` 为进行中的变更）
- AI 工具命令已配置：Kimi Code / Claude Code / Cursor / 共享 `.agents`
- 发起新变更：`/opsx:propose "想法"`（Claude）或对应工具的等价命令
- 详细约定见 `openspec/config.yaml`

## 团队协作

完整协作流程（接入步骤、propose → apply → archive 闭环、各 AI 工具命令对照、FAQ）见飞书文档：
[OpenSpec 协作指南 · Agent 挑战赛](https://dptechnology.feishu.cn/docx/PC2jds3Fjoig7NxH3vfcv9sdnhf)

本仓库即团队的单一事实来源（single source of truth），并已注册为 OpenSpec store（ID：`agent-challenge`）：成员 `git clone` 并 `openspec store register` 后，`openspec/` 目录对所有人和 AI 编码助手可见。跨仓库共享规格可进一步使用 OpenSpec Stores（beta），见 OpenSpec 文档。
