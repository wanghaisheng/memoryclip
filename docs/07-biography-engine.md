# Biography Engine

Biography Engine 负责将 Timeline 转换为可阅读的人物传记。

它不是直接生成纪录片，而是生成**结构化 Biography**。

后续 Story Engine、Documentary Engine 都依赖 Biography。

---

## Responsibilities

负责：

- 生平整理
- 自动分章节
- 生成摘要
- 人物画像
- 缺失信息提示
- 多语言传记

---

## Input

来源：

- Timeline
- Memory Graph
- Family Relationship
- Historical Context
- User Notes

---

## Output

```ts
interface Biography {

  id:string

  personId:string

  title:string

  summary:string

  chapters:BiographyChapter[]

  tags:string[]

}
```

---

## BiographyChapter

```ts
interface BiographyChapter{

  id:string

  title:string

  content:string

  timelineEventIds:string[]

}
```

---

## Default Chapters

默认生成：

```
Early Life

Education

Career

Marriage

Family

Achievements

Later Life

Legacy
```

可删除、重命名、新增。

---

## Biography Styles

支持：

```
Documentary

Family

Historical

Museum

Academic

Short
```

例如：

### Documentary

> John was born in 1932...

---

### Family

> Grandpa always loved gardening...

---

### Historical

> Born during the Great Depression...

---

## Summary

自动生成：

```text
100 words

300 words

1000 words
```

方便：

- 首页介绍
- 视频简介
- 分享卡片

---

## Missing Information

自动检测：

例如：

```
Career

Unknown

Marriage

Unknown

Military

Unknown
```

生成建议：

```
Please upload

Employment Records

Marriage Certificate

Military Photos
```

帮助用户补充资料。

---

## Evidence

每段 Biography 都可以查看来源。

例如：

```
Career

↓

Employment Certificate

↓

Interview Audio

↓

Family Note
```

点击即可查看原始素材。

---

## APIs

生成 Biography

```
POST

/api/biography/generate
```

获取

```
GET

/api/biography/:personId
```

更新

```
PATCH

/api/biography/:id
```

重新生成

```
POST

/api/biography/regenerate
```

---

## Agent

Biography Agent

负责：

- 阅读 Timeline
- 阅读 Evidence
- 整理章节
- 编写 Biography
- 检查一致性

---

## UI

```
Biography

━━━━━━━━━━━━━━

Summary

━━━━━━━━━━━━━━

Early Life

━━━━━━━━━━━━━━

Education

━━━━━━━━━━━━━━

Career

━━━━━━━━━━━━━━

Family

━━━━━━━━━━━━━━

Legacy
```

右侧显示：

```
Evidence

Timeline

Comments

History
```

---

## Dependencies

输入：

- Timeline Engine
- Memory Engine
- Historical Engine

输出：

- Story Engine
- Documentary Engine
- Search
- Export

Biography 是人物的标准文本表达，也是后续所有内容生成的基础。
