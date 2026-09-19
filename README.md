# Agent 挑战赛 · 项目管理仓库

本仓库是参加两项比赛的项目管理仓库，使用 [OpenSpec](https://github.com/Fission-AI/OpenSpec) 做规格驱动的变更管理。

## 比赛

> 题目已于 2026-09-18 20:00 在飞书群「DP-Arena内部赛」发布，要点见下表备注与 `openspec/changes/` 下的对应变更。

| 比赛 | 链接 | 备注 |
|---|---|---|
| 比赛 A（DPA4C Nano 单 PPU 生产部署优化赛） | https://play.bohrium.com/competitions/dpa | 单张 PPU810E 96GB，CuNi/Si/MgO 三材料×三规模，共九题；优化完整 LAMMPS MD 步；正确性全过后按九题三轮配对加速比的几何平均排名；交付 results.json、优化记录、构建材料、日志与真实轨迹，最终提交另需镜像及接口自测。规格：`openspec/changes/propose-dpa-md-official-task/` |
| 比赛 B（推理服务评测赛／LLM 部署赛） | https://play.bohrium.com/llm-arena/competitions/llm-deploy-arena-v1 | 固定 GLM-5.3-Flash、8×A100-SXM4-80GB；两科能力 points 均须 >95；正式隐藏会话负载按 N@SLO 降序、同档 TPOT 均值升序排名，TPM 不排名；交付 LBG 镜像引用及启动配置 submission.json、真实轨迹。规格：`openspec/changes/propose-llm-serving-official-task/` |
| 参赛指南 | https://dptechnology.feishu.cn/wiki/NevpwcEEGi2deek51TMcNTvDnAh | 注册 / Token / 赛道入口 |

正式口径来自[群内开赛指南](https://dptechnology.feishu.cn/wiki/NevpwcEEGi2deek51TMcNTvDnAh)图片指定的 Playground 任务书。邀请函中的“固定1024原子”及“评测query完全可见”属于旧摘要，不适用于上述正式评测。来源版本和哈希见两份提案的 `sources.md`。开赛时间为 2026-09-18 20:00（Asia/Shanghai）；已读公告和题面未给出确定截止时间。

**评分与轨迹规则**（不看轨迹、自由 Agent 架构、trace 文件上传绕限等）见 [docs/比赛规则说明.md](docs/比赛规则说明.md)。

## 仓库边界

本仓库是 **store 仓库**，只负责对齐需求与记录事实：比赛题目解读、方案规格、分工与进度。比赛代码**不放在这里**。

- 每个比赛项目另开独立代码仓库（多个项目则一题一仓），代码仓库只放实现
- 代码仓库需要读规格时，clone 本仓库并注册为 store：`openspec store register <path> --id agent-challenge --yes`
- 各项目代码仓库统一登记在下表，避免实现散落后找不到归属：

| 项目 | 代码仓库 | 备注 |
|---|---|---|
| 比赛 A（DPA） | 待迁出（本地工作区 `dpa4c-nano-lammps-md/`） | 赛题包已下载，OpenSpec 已初始化 |
| 比赛 B（LLM） | 待迁出（本地工作区 `llm-challenge-arena-v1/`） | 赛题包已下载，OpenSpec 已初始化 |

## 工具链约定

| 用途 | 工具 |
|---|---|
| 规格 / 变更管理 | `openspec`（本仓库） |
| Bohrium 资源（文件 / 数据集 / 任务 / 节点等） | `bohr` CLI |
| 数据集下载 | `wenyon`（`wenyon-cli`） |
| 算力资源 / Arena Team | `trisol`（审批与配额按各自账号实时查询，不能沿用其他成员状态） |

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
