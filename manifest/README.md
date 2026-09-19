# Skill Manifest

`skills.json` 是 `public` 当前使用的 Skill 清单。

每个 Skill 记录：

- 唯一 ID 和版本
- 来源类型与路径
- 能力和支持平台
- 输入输出 schema
- 外部依赖
- 是否必须人工审核

当前 `public-wechat` 使用独立本地仓库的 workspace 引用，方便同步开发。发布时改为：

```json
{
  "source": {
    "type": "git",
    "repository": "https://github.com/<owner>/public-wechat",
    "ref": "v0.1.0",
    "commit": "<locked-commit-sha>"
  }
}
```

在远程仓库和 tag 未建立前，不填写虚假的 URL 或版本。
