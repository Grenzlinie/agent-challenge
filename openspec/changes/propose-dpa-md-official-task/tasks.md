# Tasks

## 1. 规格与资源

- [ ] 1.1 团队审查本提案与旧邀请函提案冲突，记录选定版本，验证不会同时归档冲突规格。
- [ ] 1.2 建立独立比赛A实现仓库并登记README；验证store引用解析至agent-challenge。
- [ ] 1.3 核验Playground、Bohr身份与单PPU权限，下载完整题包；验证唯一根含instruction.md和asset/tools/arena.py，否则停止启动沙箱。
- [ ] 1.4 按官方Wenyon来源加载数据，验证fetch的status:passed及128个文件哈希；读取tolerances.json补足统计区间。

## 2. 基线与优化

- [ ] 2.1 跑官方selftest，验证退出码0、status:passed和correctness.passed:true。
- [ ] 2.2 分离profiling与测时，记录热点及基线环境，验证profile报告覆盖邻居表、模型和主机等待。
- [ ] 2.3 在候选路径实现一个由profiling支持的改动并同步构建材料，验证15个回归点及单场景compare通过且基线未修改。
- [ ] 2.4 跑同一版本九题evaluate，验证完整性、正确性和score.value；失败时保留报告，不拼历史成绩。

## 3. 复现与交付

- [ ] 3.1 用bohr image build构建最终镜像，从digest新建沙箱跑image-selftest，验证三个小体系全部通过并保存实际Dockerfile。
- [ ] 3.2 整理results/optimization/build/logs及image.json，验证官方package dry-run通过、轨迹真实且无凭据。
- [ ] 3.3 核对当日提交次数小于5与最终版本后提交，保存attempt_id；查状态并区分收件、自测、人工审核及最终成绩。
