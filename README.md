# Agent 挑战赛 · 项目管理仓库

本仓库是参加两项比赛的项目管理仓库，使用 [OpenSpec](https://github.com/Fission-AI/OpenSpec) 做规格驱动的变更管理。

## 比赛

> 题目于 2026-09-18 20:00 开放，开放后在此补充赛题名称与要求。

| 比赛 | 链接 | 备注 |
|---|---|---|
| 比赛 A | https://dptechnology.feishu.cn/wiki/N9STwPrFEiDLXbkSGZxcp4mFn2e | 待补充 |
| 比赛 B | https://dptechnology.feishu.cn/wiki/Pda8wY9NFiXS7xkN75qcESzXnvU | 待补充 |

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
