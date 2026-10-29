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
  function-words.md     功能词 108
  logic-words.md        逻辑词 26
  nouns.md              名词 320
  verbs.md              动词 133
  adjectives.md         形容词 84
  adverbs.md            副词 30
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

1. **词条 = 词形 + 义项**。同一词形的不同义项分行立条，用 ¹ ² 上标标记，不得合并。
   - 例：`light¹`（光）/ `light²`（轻）；`right¹`（正确）/ `right²`（右边）/ `right³`（权利）。
2. **一词性多值**：同一义项允许兼类（如 `before` 兼介词、连词、副词），不同义项不可合并。
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

## 多义词登记

下表记录全部分行立条的词形，防止回改时被误合并。

| 词形 | 义项 A | 义项 B | 义项 C | 处理 |
|---|---|---|---|---|
| light | light¹ 光（n.） | light² 轻（adj.） | — | 分行 |
| right | right¹ 正确（adj.） | right² 右边（n./adj.） | right³ 权利（n.） | 分行 |
| back | back¹ 背部（n.） | back² 回（adv.） | — | 分行 |
| hard | hard¹ 困难（adj.） | hard² 坚硬（adj.） | — | 分行 |
| free | free¹ 自由（adj.） | free² 免费（adj.） | — | 分行 |
| open | open¹ 打开（v.） | open² 开着的（adj.） | — | 分行 |
| orange | orange¹ 橙子（n.） | orange² 橙色（adj.） | — | 分行 |
| no | no¹ 没有（det.） | no² 不（adv.） | — | 分行 |
| her | her¹ 她（pron.） | her² 她的（det.） | — | 分行 |
| that | that¹ 那个（det.） | that² 引导从句（conj.） | — | 分行 |
| order | order¹ 命令（n.） | order² 顺序（n.） | — | 分行 |
| letter | letter¹ 信（n.） | letter² 字母（n.） | — | 分行 |
| call | call¹ 叫（v.） | call² 打电话（v.） | — | 分行 |
| like | like¹ 喜欢（v.） | like² 像（prep.） | — | 分行 |
| so | so¹ 所以（conj.） | so² 这么（adv.） | — | 分行 |
| own | own¹ 自己的（adj.） | own² 拥有（v.） | — | 分行 |
| glass | glass¹ 玻璃（n.） | 玻璃杯 | — | 只留 A，杯子用 cup |
| lie | lie¹ 躺（v.） | lie² 谎言（n.） | 说谎 | 只留 A、B，说谎用 tell lie |
| watch | watch¹ 手表（n.） | 观看（v.） | — | 只留 A，观看用 look |
| close | close¹ 关（v.） | 近的（adj.） | — | 只留 A，近用 near |
| point | point 点（n.） | 指（v.） | — | 只留 A |
| second | second¹ 秒（n.） | 第二（num.） | — | 第二由数词规则生成 |
| play | play 玩；演奏（v.） | — | — | 同一义项的两用法，合并 |
| before/after | 在……前/后 | — | — | 同一义项兼介词、连词、副词 |
| work | work¹ 工作（n.） | work² 工作（v.） | — | 同义兼类，分列便于检索 |
| answer | answer 回答（n./v.） | — | — | 同义兼类，分列便于检索 |

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
| 功能词 | [function-words.md](./core-word/function-words.md) | 108 |
| 逻辑词 | [logic-words.md](./core-word/logic-words.md) | 26 |
| 名词 | [nouns.md](./core-word/nouns.md) | 320 |
| 动词 | [verbs.md](./core-word/verbs.md) | 133 |
| 形容词 | [adjectives.md](./core-word/adjectives.md) | 84 |
| 副词 | [adverbs.md](./core-word/adverbs.md) | 30 |
| **合计** | [index.md](./core-word/index.md) | **701** |

旧版 138 词（名词 52 / 动词 35 / 形容词 37 / 逻辑词 14），无功能词、无多义拆分、无规则约定。本版补齐功能词与缺失语义场，并按义项拆分。

## 路线图

- [x] 基表 v2.0：701 词条，按词类拆分为独立文件
- [x] 复数规则：一条规则、零例外（`rules/04-plural.md`）
- [ ] 其余五条规则正文与反例
- [ ] 标准英语 → 简化英语映射表
- [ ] 覆盖率校验脚本
