# Memory Engine

Memory Engine 是整个 MemoryClip 的入口。

职责只有一个：

> 将各种非结构化记忆转换成结构化 Memory Graph。

---

## 输入

支持：

- 墓碑照片
- 老照片
- 视频
- 音频
- 信件
- 日记
- PDF
- Word
- 家谱
- 用户手工输入

---

## 输出

统一输出：

```ts
interface MemoryNode {
  id:string

  type:
    | "person"
    | "event"
    | "place"
    | "asset"

  confidence:number

  evidence:string[]

  metadata:Record<string,any>
}
```

---

## Pipeline

```
Upload

↓

OCR

↓

Metadata

↓

Entity

↓

Relationship

↓

Timeline

↓

Memory Graph
```

---

## OCR

识别：

- 墓碑
- 信件
- 手写
- PDF
- 证件

输出：

```json
{
  "text":"",
  "confidence":0.98
}
```

---

## Face Recognition

提取：

- 人物
- 年龄
- 性别
- 表情

输出：

```json
{
  "personId":"",
  "age":25
}
```

---

## Relationship Extraction

识别：

```
Father

Mother

Son

Teacher

Friend
```

生成：

```
Person A

↓

Father

↓

Person B
```

---

## Timeline Builder

自动排序：

```
1932

↓

1948

↓

1952

↓

1960
```

---

## API

POST

```
/api/memory/upload
```

POST

```
/api/memory/analyze
```

GET

```
/api/memory/:id
```

---

## Agent

负责：

Memory Agent

调用：

OCR

Vision

LLM

Embedding

最后写入：

Memory Graph
