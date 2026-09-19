# Tasks

任务是一次宣传内容生产运行，不是一个平台 Skill。

## 最小任务阶段

```text
intake -> fact_check -> brief_ready -> adapting -> review -> approved -> exported
```

每个任务至少保存：

- `brief.json`
- `sources.json`
- 各平台 `platform-result`
- `review.json`

平台结果应独立保存。一个平台失败时，其他平台仍可审核和导出。
