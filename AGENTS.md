# Agent Rules

开始任务前先读取 `PROJECT-DEVELOPMENT-ZEN.md`、`README.md` 和相关 Skill。

- `public` 只负责总入口、模块注册、任务编排和公共协议。
- 独立 Skill 保留在自己的仓库，禁止复制源码到本仓库。
- 只修改当前 worktree，不修改正式环境、正式配置或密钥。
- 一个任务一个 feature 分支；未经明确要求，不 commit、push、merge 或 release。
- 修改完成后运行 `scripts/verify`，报告文件、验证结果、剩余问题和风险。
