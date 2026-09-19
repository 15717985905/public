# public

面向宣传、包装和自我营销的模块化内容创作总工具。

`public` 负责理解任务、组织材料、选择 Skill 和汇总结果。具体平台能力保持独立，例如：

- `public-wechat`：科研成果和长文公众号推文
- `public-xiaohongshu`：短标题、卡片和图文笔记
- `public-weibo`：短文案、话题和实时传播
- `public-zhihu`：问题导向、论证和引用

## 核心流程

```text
原始材料
  -> 事实与来源
  -> content brief
  -> 目标平台 Skill
  -> 平台质检
  -> 人工终审
  -> 本地输出
```

一份材料只做一次事实核查。不同平台只调整表达、结构和输出格式，不擅自改变已核实事实。

## 仓库关系

`public` 与平台 Skill 分开维护：

- Skill 可以单独安装和调用。
- `public` 通过 `manifest/skills.json` 引用 Skill，不复制源码。
- Skill 可以独立升级；`public` 再更新所使用的版本或 commit。
- 公开发布前，workspace 引用必须替换为远程仓库 URL 和稳定 tag。

当前接入的 `public-wechat` 仍处于本地开发状态，见 `manifest/skills.json`。

## 当前状态

- 总入口协议：已建立
- Skill 注册表：已建立
- `public-wechat`：本地 workspace 接入
- 其他平台：尚未实现
- 自动发布：暂不实现

## 验证

```bash
bash scripts/verify
```

最小输入示例见 `examples/content-brief.json`。
