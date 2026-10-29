# 04 · 复数规则

> 状态：v2.0 生效中 · 依赖：`core-word/` 下的词表
> 原则：**一条规则，零词法例外**。任何名词的复数都能由规则直接算出，学习者不需要记忆任何特殊形式。

## 1. 规则

```
复数 = 词干 + es
      若词干以 e 结尾，则为 词干 + s
```

只有这一条。没有 `-ies`、没有 `-ves`、没有 `people / children / mice`。

| 步骤 | 操作 | 示例 |
|---|---|---|
| 1 | 取单数词干 | `person` |
| 2 | 末字母是 e？是 → + s；否 → + es | `person` 不以 e 结尾 → `persones` |
| 3 | 名词前有大于 1 的数量词时，必须带复数标记 | `two persones` |

> 第 2 步的“e 结尾只加 s”是**拼写规则**，不是词法例外：它只避免 `housees` 这种连续三个元音字母的写法，任何词都按同一判据处理，不需要记单词。

## 2. 为什么这样改

传统英语的复数其实也只有一条生产性规则（`-s`，咝音后 `-es`），真正的问题不是规则，而是**词法例外**：`person → people`、`child → children`、`mouse → mice`。这些词必须逐个背，破坏了“基”的可组合性。

本规则把两件事一起压平：

1. 后缀只有一个：`es`；
2. 例外一个不留：所有名词都走同一条路。

代价是拼写与标准英语不同（`persones`、`piges`、`bookes`），收益是**零记忆成本**：知道单数就必然知道复数。

## 3. 应用表

### 3.1 一般词尾

| 单数 | 复数 | 说明 |
|---|---|---|
| pig | piges | |
| dog | doges | 与 doge 的复数同形，见 §5 |
| person | persones | 取代 people |
| book | bookes | |
| cup | cupes | |
| table | tables | e 结尾 → +s |
| house | houses | e 结尾 → +s |
| cake | cakes | e 结尾 → +s |

### 3.2 咝音词尾（结果与传统英语一致）

| 单数 | 复数 |
|---|---|
| bus | buses |
| box | boxes |
| glass | glasses |
| watch | watches |
| fish | fishes |
| dish | dishes |

### 3.3 被废除的不规则形式

| 单数 | 传统复数 | 新规则 |
|---|---|---|
| person | people | **persones** |
| man | men | **manes** |
| woman | women | **womanes** |
| child | children | **childes** |
| tooth | teeth | **toothes** |
| foot | feet | **footes** |
| mouse | mice | **mouses** |
| sheep | sheep | **sheepes** |
| leaf | leaves | **leafes** |
| knife | knives | **knifes** |
| life | lives | **lifes** |
| half | halves | **halfes** |
| city | cities | **cityes** |
| baby | babies | **babyes** |
| fish | fish | **fishes** |

> 注意：`knife`、`life` 以 e 结尾，按规则只加 s：`knifes`、`lifes`。传统英语的 `f → v` 变化不是规则，而是词法例外，全部取消。

### 3.4 不可数名词

`water`、`rice`、`money`、`meat` 这类不可数名词不取复数——这不是语法例外，而是语义事实（它们没有“一个/两个”的计数单位）。计量用容器或单位词：

```
two cupes of water
three bagges of rice
```

## 4. 与数量词的配合

| 数量 | 名词形式 | 例句 |
|---|---|---|
| one | 单数 | one pig |
| two 及以上 | 复数 | two piges |
| 不确定 | 复数 | many piges |
| 零 | 复数 | zero piges |

## 5. 同形碰撞清单

统一加 `es` 会让少数新形式与既有单词同形。当前登记如下，处理原则是**靠上下文与数量词消歧，不为个别词开例外**。

| 新形式 | 碰撞对象 | 处理 |
|---|---|---|
| manes | mane（鬃毛）的复数 | 数量词 + 上下文；必要时 man → male person |
| doges | doge（威尼斯总督） | 专名，不入基表，可忽略 |
| lifes | 无（`lives` 已随三单取消而消失） | 无冲突 |
| toothes | 无 | 无冲突 |
| sheepes | 无 | 无冲突 |

> 若碰撞在实际语料中造成真实歧义，优先改写句子（加 `male / female`、改用 `person`），而不是给单词加例外。

## 6. 连锁影响（必须同步）

复数只是屈折体系的一环。如果只有复数统一、其余仍保留例外，整个“基”仍然不闭合。后续规则按同一原则处理：

| 范畴 | 统一规则 | 示例 | 文件 | 状态 |
|---|---|---|---|---|
| 复数 | +es（e 结尾 +s） | persones | 本文件 | 已定 |
| 第三人称单数 | **取消** -s，动词用原形 | he go、she have | 05-tense | 待定 |
| 过去式 | +ed | goed、eated、taked | 05-tense | 待定 |
| 进行式 | +ing（e 结尾去 e） | maked → making | 05-tense | 待定 |
| 比较级 / 最高级 | +er / +est | gooder、goodest | 06-adjective | 待定 |
| 序数 | +th | oneth、twoth、threeth | 04 本文件 | 已定 |
| 系动词 be | 统一为 be？ | I be、he be | 待决策 | 待定 |

### 6.1 代词为什么不适用

`I / me / my`、`he / him / his` 在基表里是**各自独立的词条**（基元），不是同一个词的屈折形式。所以它们不构成“不规则”，也不需要规则统一。`they / them / their` 同理：三个基元，不是 `he` 的派生。

这条区分很重要：**基元可以彼此无规律，派生必须绝对规律。**

## 7. 设计取舍：`-es` 还是 `-s`

| 方案 | 示例 | 优点 | 代价 |
|---|---|---|---|
| 统一 `-es`（当前） | persones、piges、bookes | 单后缀，规则最短 | 与标准拼写差异大；manes / doges 碰撞 |
| 统一 `-s` | persons、pigs、books | 更接近传统拼写，碰撞少 | 咝音词需写 `boxs`、`buss`，可读性更差 |

当前选择 `-es`：它让“复数标记”在视觉上更醒目（`piges` 一眼看出是复数），且咝音词结果与传统英语一致。若要切换到 `-s`，只需修改 §1 的后缀并重跑映射表，基表本身不动。

## 8. 验收清单

- [ ] 随机抽 20 个基表名词，套用规则生成复数，人工可读性打分（1–5）
- [ ] 统计全表碰撞词数量（当前 2 个）
- [ ] 确认 `rules/examples/` 中所有例句的复数都按本规则书写
- [ ] 与 `rules/05-tense.md` 的动词规则联调，确认 `lifes / lives` 类冲突已消除
