# Skill 接入协议

一个独立 Skill 要能单独调用，也要能被 `public` 组合调用。

## Skill 最小要求

独立仓库至少提供：

```text
SKILL.md
README.md
CHANGELOG.md
```

`SKILL.md` 使用 frontmatter 声明：

```yaml
---
name: public-wechat
version: 0.1.0
description: ...
capabilities:
  - wechat-article-generation
platforms:
  - wechat
requires_human_review: true
---
```

平台专属脚本、模板、图片和示例只放在 Skill 自己的仓库。

## 总项目接入字段

`manifest/skills.json` 记录：

- `id`：稳定的 Skill 名称
- `version`：当前使用版本
- `source`：workspace 或 git
- `capabilities`：可路由的能力
- `platforms`：支持的平台
- `input_schema`、`output_schema`：契约路径
- `requires_human_review`：是否必须人工终审
- `dependencies`：运行前置条件

## 调用边界

总入口先生成或补全 `content-brief`，再根据 manifest 中的 `input_mode` 把公共 brief 映射到 Skill 的原生输入。比如论文 Skill 还需要 PDF 和通讯作者资料。Skill 返回 `platform-result`，不直接修改其他平台结果，也不自动发布。

每个平台失败时保留其他平台产物。错误写入该平台自己的结果，不把失败静默成成功。

## 版本规则

- Skill 自己使用 SemVer 和 Git tag。
- `public` 只更新 manifest 中的版本或 commit。
- schema 发生不兼容变化时，先升级协议版本，再升级 Skill。
- workspace 引用只用于本地开发，发布前必须换成远程仓库和锁定 commit。
