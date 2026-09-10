# 飞书多维表数据看板 · 集成测试

从飞书多维表真实拉取渲染的看板页面，用于验证《多维表数据看板集成 SOP》中的各项能力。

- 入口：`index.html`（数据已内联，无需后端）
- `data.json`：构建时的数据快照，供对照
- 已脱敏：不含 base token、表 ID、租户地址

## 验证要点（页面内悬停即看，无需点击）

| 项 | 验证方式 |
| --- | --- |
| 字段解析 | 悬停任意单元格 → 对照「接口原始值 / 页面解析值」 |
| 数据新鲜度 | 悬停右上角新鲜度徽标 → 拉取时间、阈值、降级原因 |
| 数据契约 | 改 Base 字段名后重新构建 → 契约面板报警，缺失槽位显示 `—` |
| 失败降级 | 断网构建 → 保留上次快照并标记「降级快照」，不假报成功 |

## 本地重建

```bash
node fetch-and-build.js              # 拉取 + 重建
node fetch-and-build.js --offline    # 只改样式，不联网
node fetch-and-build.js --publish     # 额外产出脱敏版到 out/publish/
node test/field-adapter.test.js      # 字段解析单测
```
