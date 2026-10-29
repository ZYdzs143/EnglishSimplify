# EnglishSimplify · 英语简化计划

用“基”的思想重构英语词表：先确定一组不可再分解的基本词，其余词汇全部由基本词按规则组合生成。

```
pork      →  pig meat
beef      →  cow meat
mutton    →  sheep meat
chicken   →  chicken meat
```

与中文“猪 + 肉 = 猪肉”的构词方式一致：不背新词，只学组合。

派生同样只有一条规则，没有例外：

```
person → persones      child → childes      mouse → mouses
good   → gooder        first → oneth        well  → goodly
```

## 目录结构

```
core-word/              基本单词（每个文件只有词与释义）
  index.md              词表索引
  function-words.md     功能词 106
  logic-words.md        逻辑词 25
  nouns.md              名词 317
  verbs.md              动词 131
  adjectives.md         形容词 84
  adverbs.md            副词 27
rules/
  04-plural.md          复数规则
  examples/             组合示例（待建）
```

设计约定、多义词登记、待定项全部放在本文件；`core-word/` 下的词表只保留“词 + 释义”。

## 三条设计原则

| 条件 | 数学表述 | 词汇学表述 | 本表如何落实 |
|---|---|---|---|
| 无关性 | 基向量线性无关 | 任一基词不能由其他基词组合定义，否则循环定义 | 一词一义；近义词只留一个；派生、屈折不入表 |
| 张成性 | 空间内任一向量可写作基的线性组合 | 目标词表（牛津 3000 / COCA 5000）中的词都能被分解 | 覆盖率脚本验证（待建） |
| 唯一性 | 坐标唯一 | 每个概念只有一种规范写法 | 组合规则必须确定，禁止同义变体 |

唯一性最容易被忽略：若 `pork` 可以写成 `pig meat` / `meat of pig` / `pig's meat`，这套语言就退化成方言，既教不会人，也无法让程序互转。

## 词条约定

1. **一词一义**：一个拼写只承担一个义项。同形不同义时**不用上标**，改用换词、组合或造词（见「一词一义」一节）；同一义项在不同词性下可共用拼写（兼类）。
2. **兼类**：同一义项可在不同词性下共用拼写（如 `open` 动词/形容词、`work` 名词/动词、`before` 介词/连词/副词）；不同义项不可共用拼写。
3. **只收基词**：派生词（-er / -ly / -less / un- / re-）与复合词（`pig meat`、`water bottle`）不入表，由 `rules/` 生成。
4. **屈折不入表**：复数、过去式、-ing、比较级、序数一律由规则生成，**不保留任何不规则形式**。
5. **收词标准**：a) 高频；b) 语义稳定、不易漂移；c) 无法用本表更简单的词稳定替代。
6. **释义用本表词写**：逐词补英文释义时做循环性检查（定义中不得出现被定义词及其派生）。
7. **代词是基元**：`I / me / my`、`he / him / his` 在表内是各自独立的词条，不是同一个词的屈折形式——**基元之间可以无规律，派生必须绝对规律**。

## 词表之外的约定

这些规则不占词条，统一写在这里：

| 对象 | 规则 |
|---|---|
| 不定冠词 | 辅音前 `a`，元音前 `an`（表中合并为一条 `a/an`） |
| 系动词 be | 屈折为 am / is / are / was / were / been / being |
| 反身代词 | 物主词 + `self`：my self、your self、him self |
| 指示词 | 不随数变化：`this bookes`、`that piges`；`these` / `those` 废除 |
| 序数 | 数词 + `th`：oneth、twoth、threeth（first / second / third 废除） |
| 方式副词 | 形容词 + `ly`：goodly、slowly、happily（`well` 废除） |
| 第三人称单数 | 建议取消 -s，动词用原形：he go、she have（待定，见规则 05） |

## 派生规则

### 复数（`rules/04-plural.md`）

```
复数 = 词干 + es；词干以 e 结尾时 + s
```

| 单数 | 新复数 | 被废除的传统形式 |
|---|---|---|
| person | persones | people |
| child | childes | children |
| man / woman | manes / womanes | men / women |
| tooth / foot | toothes / footes | teeth / feet |
| mouse | mouses | mice |
| sheep | sheepes | sheep（单复数同形） |
| leaf / knife / life | leafes / knifes / lifes | leaves / knives / lives |
| city / baby | cityes / babyes | cities / babies |

- 唯一保留的拼写处理：词干以 `e` 结尾只加 `s`（`house → houses`），避免三个元音连写。
- 同形碰撞：`manes`（鬃毛复数）、`doges`（doge）。处理原则是改写句子，不给单词开例外。

### 其他屈折（待定）

| 范畴 | 统一规则 | 示例 | 状态 |
|---|---|---|---|
| 过去式 | +ed | goed、eated、taked | 待定 |
| 进行式 | +ing（e 结尾去 e） | maked → making | 待定 |
| 比较级 / 最高级 | +er / +est | gooder、goodest | 待定 |
| 第三人称单数 | 取消 -s | he go | 待定 |
| 系动词 be | 统一为 be？ | I be、he be | 待决 |

## 一词一义

一个拼写只承担一个义项。同形不同义时**不使用上标**，按以下优先级处理：

1. **换词**：英语已有现成且不冲突的词，直接采用（`light` 光 → `shine`）。
2. **组合**：由基词组合表达，不新增词条（谎言 → `false word`，权利 → `law power`）。
3. **造词**：以上都不合适时新造，拼写须符合英语音节习惯（她的 → `hir`）。

同一义项在不同词性下共用拼写（兼类）是允许的，例如 `work`（n./v. 工作）、`open`（v./adj. 开）；不同义项绝不共用拼写。

### 原同形词的处理

| 原写法 | 义项 A | 义项 B | 义项 C | 处理 |
|---|---|---|---|---|
| light | 光 | 轻 | — | 光 = shine；轻 = light |
| right | 正确 | 右边 | 权利 | 正确 = correct；右边 = right；权利 = law power（组合） |
| free | 自由 | 免费 | — | 自由 = free；免费 = gratis |
| hard | 困难 | 坚硬 | — | 困难 = difficult；坚硬 = hard |
| letter | 信 | 字母 | — | 信 = mail；字母 = letter |
| order | 命令 | 顺序 | — | 命令 = command；顺序 = order |
| call | 叫 | 打电话 | — | 叫/称呼 = name；打电话 = call |
| lie | 躺 | 谎言 | — | 躺 = lie；谎言 = false word（组合） |
| orange | 橙子 | 橙色 | — | 橙子 = orange；橙色 = orange color（组合） |
| back | 背 | 回 | — | 背 = back；回 = return |
| no | 没有 | 不 | — | 没有 = no；不 = not |
| like | 喜欢 | 像 | — | 喜欢 = like；像 = as |
| so | 所以 | 这么 | — | 所以 = so；这么 = this（this big） |
| too | 太 | 也 | — | 太 = too；也 = also |
| that | 那个 | 引导从句 | — | 那个 = that；从句连词直接省略 |
| her | 她 | 她的 | — | 她 = her；她的 = hir（造词） |
| clean | 干净的 | 打扫 | — | 干净 = clean；打扫 = make clean（组合） |
| own | 自己的 | 拥有 | — | 自己的 = own；拥有 = have |
| open | 打开 | 开着的 | — | 同一义项，兼类不拆 |
| play | 玩 | 演奏 | — | 玩 = play；演奏 = play music（组合） |

### 新增与替换词

| 词 | 词性 | 释义 | 方式 |
|---|---|---|---|
| shine | n. | 光 | 换词（原 light 的光义） |
| mail | n. | 信 | 换词（原 letter 的信义） |
| command | n. | 命令 | 换词（原 order 的命令义） |
| correct | adj. | 正确的 | 换词（原 right 的正确义） |
| difficult | adj. | 困难的 | 换词（原 hard 的困难义） |
| gratis | adj. | 免费的 | 换词（原 free 的免费义） |
| hir | det. | 她的 | 造词（原 her 的她的义） |
| name | v. | 称呼 | 兼类扩展（原 call 的叫义） |

### 词条数变化

| 项目 | 数量 |
|---|---|
| 旧版 | 701 |
| 删除（改由组合表达） | 11 |
| 替换（不增不减） | 8 |
| **现版** | **690** |

## 待定与排除

### 明确排除

- 专有名词：人名、地名、国名、品牌名不入表，另建专名表。
- 缩写与符号：`TV`、`OK`（已入 okay）、单位符号等。

### 借词层（待决策）

`computer`、`phone`、`coffee`、`pizza`、`radio`、`internet` 这类词有两个方案：

1. **借词层**：承认它们不可分解，单列一张“技术借词表”，与基表隔离；
2. **构词**：`computer` = thinking machine、`phone` = far-speak machine、`internet` = world net。

建议先用方案 1 保证可用，再逐步用方案 2 替换，并把替换结果记入映射表。

### 待验证的组合方案

| 对象 | 拟用方案 | 风险 |
|---|---|---|
| 11–99 数词 | `two-ten`、`three-ten-five` | 与基数词读音差异大，需母语者可读性测试 |
| 星期 | `day one` … `day seven` | 与“第一天”歧义 |
| 月份 | `month one` … `month twelve` | 同上 |
| 今天/明天/昨天 | `this day / next day / last day` | 与“下一天”歧义 |

### 待补规则

- 派生：`-er`（做……的人）、`-ly`（……地）、`-less`（没有……的）、`un-`（不……）、`re-`（再……）。
- 复合词长度上限（建议 ≤ 3 个基词），超出改用 `of / for` 短语，避免名词串歧义。

## 统计

| 类别 | 文件 | 词条数 |
|---|---|---|
| 功能词 | [function-words.md](./core-word/function-words.md) | 106 |
| 逻辑词 | [logic-words.md](./core-word/logic-words.md) | 25 |
| 名词 | [nouns.md](./core-word/nouns.md) | 317 |
| 动词 | [verbs.md](./core-word/verbs.md) | 131 |
| 形容词 | [adjectives.md](./core-word/adjectives.md) | 84 |
| 副词 | [adverbs.md](./core-word/adverbs.md) | 27 |
| **合计** | [index.md](./core-word/index.md) | **690** |

旧版 138 词（名词 52 / 动词 35 / 形容词 37 / 逻辑词 14），无功能词、无多义拆分、无规则约定。本版补齐功能词与缺失语义场，并按义项拆分。

## 路线图

- [x] 基表 v2.0：690 词条，按词类拆分为独立文件
- [x] 复数规则：一条规则、零例外（`rules/04-plural.md`）
- [ ] 其余五条规则正文与反例
- [ ] 标准英语 → 简化英语映射表
- [ ] 覆盖率校验脚本