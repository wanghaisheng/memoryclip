# Timeline Engine

Timeline Engine 负责构建人物一生的时间轴。

整个系统只有一个时间线。

Biography、Story、Documentary 都基于 Timeline。

---

## Responsibilities

负责：

- 提取时间
- 合并事件
- 排序
- 去重
- 时间推断
- 冲突检测

---

## Input

来源：

- OCR
- 用户输入
- Biography
- Documents
- Photos
- Video Metadata
- Audio Transcript

---

## Output

```ts
interface TimelineEvent {
  id:string

  title:string

  start:string

  end?:string

  location?:string

  people:string[]

  assets:string[]

  confidence:number

  evidence:string[]
}
```

---

## Example

输入：

```
毕业证

1954

↓

结婚证

1961

↓

退休证

1988
```

输出：

```
1932

出生

↓

1954

大学毕业

↓

1961

结婚

↓

1963

长子出生

↓

1988

退休

↓

2015

逝世
```

---

## Event Types

支持：

```
Birth

Education

Career

Military

Marriage

Children

Migration

Award

Travel

Illness

Retirement

Death

Legacy
```

---

## Date Precision

支持不同精度。

```
1992

1992-05

1992-05-12

Spring 1992

Around 1992
```

系统保存：

```ts
precision:
"year"
"month"
"day"
"estimated"
```

---

## Conflict Detection

例如：

```
出生：

1932

↓

身份证：

1933
```

输出：

```
Conflict

Need Review
```

不会自动覆盖。

---

## Timeline Merge

多个来源：

```
OCR

+

Family

+

Archive
```

↓

```
One Timeline
```

每条记录保留来源。

---

## Confidence

每个事件都有可信度。

```
100%

官方证件

95%

墓碑

80%

家庭口述

60%

AI 推断
```

---

## APIs

获取时间线

```
GET

/api/timeline/:projectId
```

新增事件

```
POST

/api/timeline
```

更新

```
PATCH

/api/timeline/:id
```

删除

```
DELETE

/api/timeline/:id
```

重新排序

```
POST

/api/timeline/sort
```

---

## Agent

Timeline Agent

负责：

- Merge
- Sort
- Detect Conflict
- Normalize
- Build Timeline

---

## UI

Timeline 页面：

```
━━━━━━━━━━━━━━━

1932

Born

━━━━━━━━━━━━━━━

1954

Graduation

━━━━━━━━━━━━━━━

1961

Marriage

━━━━━━━━━━━━━━━

1988

Retirement

━━━━━━━━━━━━━━━

2015

Legacy
```

支持：

- 拖拽排序
- 编辑
- 评论
- 查看证据
- 跳转素材

---

## Dependencies

输入：

- Memory Engine

输出：

- Biography Engine
- Story Engine
- Documentary Engine

Timeline 是整个 MemoryClip 的唯一时间来源。
