---
name: public
version: 0.1.0
description: 识别宣传内容创作需求，整理事实和传播策略，并按平台调用独立 Skill 生成可审核的宣传内容；适用于科研成果、产品、品牌、活动、招生和个人品牌传播。
capabilities:
  - content-brief-orchestration
  - platform-skill-routing
  - multi-platform-content-planning
platforms:
  - generic
requires_human_review: true
---

# public 总入口

`public` 只做总入口和编排。具体平台规则由 `manifest/skills.json` 中的独立 Skill 负责。

公共 brief 不是所有 Skill 的唯一输入。manifest 若声明 `native_plus_brief`，总入口必须同时提供该 Skill 的原生材料，例如论文 PDF、作者资料或产品图片。

## 工作流程

```text
理解需求
→ 补齐目标、受众、材料和平台
→ 提取来源与可验证声明
→ 生成 content brief
→ 按 manifest 映射 Skill 原生输入
→ 选择一个或多个平台 Skill
→ 收集 platform result
→ 统一检查事实和审核状态
→ 输出本地文件
```

## 路由维度

同时判断：

- `content_type`：科研成果、产品、品牌、活动、招生或个人品牌
- `objective`：认知、解释、信任、转化、招聘、发布或声誉
- `audience`：谁会阅读和采取行动
- `platforms`：公众号、小红书、微博、知乎或其他平台

不能只根据平台名称路由。优先匹配 `content_type + objective + platform`，再读取 Skill 的 `capabilities`。

## 事实边界

- 原始材料先进入来源清单。
- 每个核心声明必须能回到一个或多个来源。
- 未核实内容不得写成确定事实。
- 平台 Skill 可以改写结构和语气，不得擅自改变已核实事实。
- 有版权或账号风险时，输出草稿并要求人工确认，不自动发布。

## 人工审核

保留两个审核节点：

1. 事实审核：确认内容是否真实、来源是否足够。
2. 发布审核：确认平台版本是否适合发布、图片和版权是否允许使用。

只有 `requires_human_review` 为 false 且项目明确允许时，才可以跳过第二个节点。当前默认必须人工终审。

## 失败处理

- 单个平台失败不影响其他平台结果。
- 失败结果必须保留错误原因和输入摘要。
- 不自动替换成未经用户确认的其他 Skill。
- 缺少材料时先询问，不猜测关键事实。

## 输出目录建议

```text
output/<task-id>/
├── brief.json
├── sources.json
├── review.json
└── platforms/
    ├── wechat/
    ├── xiaohongshu/
    └── ...
```

当前版本只定义协议和路由规则，不实现平台登录、自动发布、数据库或 Web UI。
