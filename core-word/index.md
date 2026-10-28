# 简化英语基表 · Core Word Basis

**版本** v2.0 · 2026-10-28
**规模** 702 词条（明细见 §10 统计）
**定位** 整个简化英语计划的“基”：表中每个词都不由更简单的词组合定义；表内词经 `rules/` 中的规则组合，生成其余全部词汇。

---

## 0. 为什么是“基”

借用线性代数的三个条件，一个词表要成为“基”，必须同时满足：

| 条件 | 数学表述 | 词汇学表述 | 本表如何落实 |
|---|---|---|---|
| 无关性 | 基向量线性无关 | 任一基词不能由其他基词组合定义，否则循环定义 | 一词一义；近义词只留一个；派生、屈折不入表 |
| 张成性 | 空间内任一向量可写作基的线性组合 | 目标词表（牛津 3000 / COCA 5000）中的词都能被分解 | 覆盖率脚本验证（待建） |
| 唯一性 | 坐标唯一 | 每个概念只有一种规范写法 | 组合规则必须确定，禁止同义变体 |

第三条最容易被忽略。若 `pork` 可写成 `pig meat`、`meat of pig`、`pig's meat` 三种，基就退化成方言：既教不会人，也无法让程序互转。**规范形（canonical form）与词表同等重要。**

## 1. 词条约定

1. **词条 = 词形 + 义项**。同一词形的不同义项必须分行，用 ¹ ² 上标标记，不得合并。
   - 例：`light¹`（光）/ `light²`（轻）；`right¹`（正确）/ `right²`（右边）/ `right³`（权利）。
2. **一词性多值**：同一义项允许兼类（如 `before` 兼介词、连词、副词），词性栏并列书写；不同义项不可合并兼类。
3. **只收基词**：派生词（-er / -ly / -less / un- / re-）与复合词（`pig meat`、`water bottle`）不入表，由 `rules/` 生成。
4. **屈折不入表**：复数、过去式、-ing、比较级/最高级由 `rules/04`、`rules/05` 生成；不规则形式（people、teeth、feet、better、first…）在规则文件中单独登记。
5. **收词标准**：a) 高频；b) 语义稳定、不易漂移；c) 无法用本表更简单的词稳定替代。
6. **释义用本表词写**：逐词文件阶段补做循环性检查（definition circularity check）。
7. **层级**：功能词（句法骨架）→ 逻辑词（连接与疑问）→ 名词（语义场）→ 动词 → 形容词 → 副词。

---

## 2. 功能词

功能词不指称事物，但决定“谁、对谁、做了什么”。它们是句法骨架，几乎不可再分解。

### 2.1 人称代词与反身

| 词 | 词性 | 义项 |
|---|---|---|
| I | pron. | 我（主格） |
| me | pron. | 我（宾格） |
| you | pron. | 你；你们 |
| he | pron. | 他（主格） |
| him | pron. | 他（宾格） |
| she | pron. | 她（主格） |
| her¹ | pron. | 她（宾格） |
| her² | det. | 她的 |
| it | pron. | 它 |
| we | pron. | 我们（主格） |
| us | pron. | 我们（宾格） |
| they | pron. | 他们；她们；它们（主格） |
| them | pron. | 他们；她们；它们（宾格） |
| my | det. | 我的 |
| your | det. | 你的；你们的 |
| his | det. | 他的 |
| its | det. | 它的 |
| our | det. | 我们的 |
| their | det. | 他们的 |
| self | n. | 自己（反身由“物主词 + self”生成：my self 我自己） |
| this | det./pron. | 这；这个 |
| that | det./pron. | 那；那个 |
| other | adj./pron. | 别的；其他 |
| same | adj. | 相同的 |
| such | det. | 这样的 |

> 复数形式 `these / those` 由 `rules/04` 生成，不立条。

### 2.2 冠词与限定词

| 词 | 词性 | 义项 |
|---|---|---|
| a/an | art. | 一个（不定冠词；元音前用 an） |
| the | art. | 这；那（定冠词，指已知） |
| all | det. | 全部 |
| some | det. | 一些 |
| any | det. | 任何；一些（用于疑问、否定） |
| no¹ | det. | 没有 |
| every | det. | 每个 |
| both | det. | 两个都 |
| few | det. | 很少（可数） |
| many | det. | 很多（可数） |
| much | det. | 很多（不可数） |
| more | det. | 更多 |
| most | det. | 最多 |
| less | det. | 更少 |
| least | det. | 最少 |
| enough | det. | 足够的 |
| own | adj. | 自己的 |
| whole | adj. | 整个的 |

> `each`、`several` 暂不立条，分别用 `every`、`some + 数词` 表达；见 §9 待定项。

### 2.3 数词

| 词 | 词性 | 义项 |
|---|---|---|
| zero | num. | 零 |
| one | num. | 一 |
| two | num. | 二 |
| three | num. | 三 |
| four | num. | 四 |
| five | num. | 五 |
| six | num. | 六 |
| seven | num. | 七 |
| eight | num. | 八 |
| nine | num. | 九 |
| ten | num. | 十 |
| hundred | num. | 百 |
| thousand | num. | 千 |
| million | num. | 百万 |
| half | num. | 半 |

> 11–99 拟用 `two-ten` 式组合（规则待验证）；序数 `first / second / third` 不规则，其余 -th；均登记在 `rules/04`。

### 2.4 介词

| 词 | 词性 | 义项 |
|---|---|---|
| in | prep. | 在……里 |
| on | prep. | 在……上 |
| at | prep. | 在（某点） |
| to | prep. | 到；向 |
| from | prep. | 从 |
| by | prep. | 被；由；通过 |
| with | prep. | 和；用 |
| without | prep. | 没有（语义 = with + not） |
| of | prep. | 的（所属、材料、数量） |
| for | prep. | 为；给；持续（时间） |
| about | prep. | 关于 |
| under | prep. | 在……下面 |
| over | prep. | 在……上方；超过 |
| above | prep. | 在……上方（不接触） |
| below | prep. | 在……下方 |
| between | prep. | 在……之间（两者） |
| behind | prep. | 在……后面 |
| near | prep. | 靠近 |
| through | prep. | 穿过（内部） |
| across | prep. | 横过（表面） |
| around | prep. | 围绕 |
| along | prep. | 沿着 |
| during | prep. | 在……期间 |
| against | prep. | 反对；靠着 |
| among | prep. | 在……之中（多者） |
| beside | prep. | 在……旁边 |
| toward | prep. | 朝向 |
| past | prep. | 经过 |
| out | prep./adv. | 向外；在外 |
| up | prep./adv. | 向上 |
| down | prep./adv. | 向下 |
| off | prep./adv. | 离开；脱落 |
| like² | prep. | 像 |

> `into / onto / inside / outside` 由 `in / on / out + to / side` 生成，不立条。

### 2.5 助动词与情态

| 词 | 词性 | 义项 |
|---|---|---|
| be | v./aux. | 是；在（am/is/are/was/were/been/being 为屈折） |
| do | v./aux. | 做；助动词 |
| have | v./aux. | 有；助动词 |
| can | modal | 能；可以 |
| will | modal | 将；愿意 |
| must | modal | 必须 |
| may | modal | 可以；可能 |
| should | modal | 应该 |
| would | modal | 会；愿意（will 的过去/委婉） |
| could | modal | 能（can 的过去/委婉） |

> `shall` 并入 `will`；`ought to` 并入 `should`。

### 2.6 交际用语

| 词 | 词性 | 义项 |
|---|---|---|
| yes | adv. | 是；对 |
| no² | adv. | 不（否定回答） |
| hello | int. | 你好 |
| goodbye | int. | 再见 |
| please | adv. | 请 |
| sorry | adj. | 抱歉的 |
| okay | adj./adv. | 好；可以 |

> `thank you` 由 `thank + you` 生成，不立条。

---

## 3. 逻辑词

连接与疑问是“坐标运算”的运算符：没有它们，基向量只能并列，不能成句。

### 3.1 连接词

| 词 | 词性 | 义项 |
|---|---|---|
| and | conj. | 和；并且 |
| or | conj. | 或者 |
| but | conj. | 但是 |
| so¹ | conj. | 所以 |
| because | conj. | 因为 |
| if | conj. | 如果 |
| then | adv./conj. | 然后；那么 |
| than | conj./prep. | 比 |
| as | conj./prep. | 像；作为 |
| whether | conj. | 是否 |
| although | conj. | 虽然 |
| while | conj. | 当……的时候 |
| before¹ | prep./conj./adv. | 在……之前 |
| after¹ | prep./conj./adv. | 在……之后 |
| until | prep./conj. | 直到 |
| since¹ | prep./conj. | 自从 |
| that² | conj. | 引导从句（I know that…） |

### 3.2 疑问词

| 词 | 词性 | 义项 |
|---|---|---|
| what | pron./det. | 什么 |
| who | pron. | 谁 |
| whose | pron./det. | 谁的 |
| which | pron./det. | 哪一个 |
| when | adv./conj. | 什么时候；当……时 |
| where | adv./conj. | 哪里；在……的地方 |
| why | adv. | 为什么 |
| how | adv. | 怎样；多么 |

> `when / where` 兼作连词，引导时间、地点从句；疑问与从句为同一义项，不另立条。

### 3.3 否定

| 词 | 词性 | 义项 |
|---|---|---|
| not | adv. | 不（否定动词、形容词） |

> `none` 由 `no + one` 生成；`never` 见 §7 副词。

---

## 4. 名词

名词按语义场分组。同一语义场内的词原则上互不释义，避免循环。复合名词一律不入表，只给出构词示例。

### 4.1 人

| 词 | 词性 | 义项 |
|---|---|---|
| person | n. | 人（复数 people 为不规则，登记于 rules/04） |
| man | n. | 男人；人类 |
| woman | n. | 女人 |
| child | n. | 孩子 |
| baby | n. | 婴儿 |
| boy | n. | 男孩 |
| girl | n. | 女孩 |
| family | n. | 家庭 |
| father | n. | 父亲 |
| mother | n. | 母亲 |
| son | n. | 儿子 |
| daughter | n. | 女儿 |
| brother | n. | 兄弟 |
| sister | n. | 姐妹 |
| husband | n. | 丈夫 |
| wife | n. | 妻子 |
| friend | n. | 朋友 |
| neighbor | n. | 邻居 |
| teacher | n. | 老师（亦可由 teach + -er 生成，暂留作基词） |
| student | n. | 学生 |
| doctor | n. | 医生 |
| worker | n. | 工人（work + -er 的固化形式，暂留） |
| farmer | n. | 农民（farm + -er 的固化形式，暂留） |
| king | n. | 国王 |
| leader | n. | 领袖（lead + -er 的固化形式，暂留） |

### 4.2 身体

| 词 | 词性 | 义项 |
|---|---|---|
| body | n. | 身体 |
| head | n. | 头 |
| hair | n. | 头发 |
| face | n. | 脸 |
| eye | n. | 眼睛 |
| ear | n. | 耳朵 |
| nose | n. | 鼻子 |
| mouth | n. | 嘴 |
| tooth | n. | 牙齿（复数 teeth 不规则） |
| tongue | n. | 舌头；语言（引申义暂不立条） |
| neck | n. | 脖子 |
| shoulder | n. | 肩膀 |
| arm | n. | 手臂 |
| hand | n. | 手 |
| finger | n. | 手指 |
| leg | n. | 腿 |
| foot | n. | 脚（复数 feet 不规则） |
| knee | n. | 膝盖 |
| back¹ | n. | 背部 |
| heart | n. | 心脏 |
| blood | n. | 血 |
| bone | n. | 骨头 |
| skin | n. | 皮肤 |
| brain | n. | 大脑 |

### 4.3 动物

| 词 | 词性 | 义项 |
|---|---|---|
| animal | n. | 动物 |
| dog | n. | 狗 |
| cat | n. | 猫 |
| bird | n. | 鸟 |
| fish | n. | 鱼（动物与食物同形，不另立条） |
| insect | n. | 昆虫 |
| pig | n. | 猪 → 猪肉 = pig meat |
| cow | n. | 牛 → 牛肉 = cow meat |
| sheep | n. | 羊（单复数同形）→ 羊肉 = sheep meat |
| horse | n. | 马 |
| chicken | n. | 鸡 → 鸡肉 = chicken meat（不用 chick：chick 专指雏鸡） |
| mouse | n. | 老鼠（复数 mice 不规则） |
| snake | n. | 蛇 |
| worm | n. | 虫；蠕虫 |
| bee | n. | 蜜蜂 |
| egg | n. | 蛋 |

### 4.4 植物与食物

| 词 | 词性 | 义项 |
|---|---|---|
| food | n. | 食物 |
| tree | n. | 树 |
| flower | n. | 花 |
| grass | n. | 草 |
| leaf | n. | 叶子（复数 leaves 不规则） |
| root | n. | 根 |
| seed | n. | 种子 |
| fruit | n. | 水果 |
| apple | n. | 苹果 |
| orange¹ | n. | 橙子 |
| vegetable | n. | 蔬菜 |
| grain | n. | 谷物 |
| rice | n. | 米；米饭（借词，暂留） |
| bread | n. | 面包 |
| meat | n. | 肉（食用肉） |
| milk | n. | 奶 |
| water | n. | 水 |
| salt | n. | 盐 |
| sugar | n. | 糖 |
| oil | n. | 油 |
| tea | n. | 茶（借词，暂留） |
| cake | n. | 蛋糕 |

### 4.5 自然

| 词 | 词性 | 义项 |
|---|---|---|
| nature | n. | 自然 |
| sky | n. | 天空 |
| sun | n. | 太阳 |
| moon | n. | 月亮 |
| star | n. | 星星 |
| cloud | n. | 云 |
| rain | n. | 雨 |
| snow | n. | 雪 |
| wind | n. | 风 |
| fire | n. | 火 |
| earth | n. | 地球 |
| ground | n. | 地面 |
| soil | n. | 土壤 |
| stone | n. | 石头 |
| sand | n. | 沙子 |
| sea | n. | 海 |
| river | n. | 河 |
| lake | n. | 湖 |
| mountain | n. | 山 |
| hill | n. | 小山 |
| forest | n. | 森林 |
| island | n. | 岛 |
| air | n. | 空气 |
| light¹ | n. | 光 |
| ice | n. | 冰 |
| smoke | n. | 烟 |
| shadow | n. | 影子 |

---

### 4.6 时间

| 词 | 词性 | 义项 |
|---|---|---|
| time | n. | 时间 |
| day | n. | 天；白天 |
| night | n. | 夜晚 |
| morning | n. | 早晨 |
| afternoon | n. | 下午 |
| evening | n. | 傍晚 |
| week | n. | 星期；周 |
| month | n. | 月 |
| year | n. | 年 |
| hour | n. | 小时 |
| minute | n. | 分钟 |
| second¹ | n. | 秒 |
| spring | n. | 春天 |
| summer | n. | 夏天 |
| autumn | n. | 秋天 |
| winter | n. | 冬天 |
| holiday | n. | 假日 |
| moment | n. | 时刻；片刻 |
| age | n. | 年龄 |

> `today / tomorrow / yesterday` 拟由 `this day / next day / last day` 生成（规则待验证），不立条。

### 4.7 空间与场所

| 词 | 词性 | 义项 |
|---|---|---|
| place | n. | 地方 |
| home | n. | 家 |
| house | n. | 房子 |
| room | n. | 房间 |
| door | n. | 门 |
| window | n. | 窗户 |
| wall | n. | 墙 |
| floor | n. | 地板 |
| roof | n. | 屋顶 |
| garden | n. | 花园 |
| road | n. | 路 |
| street | n. | 街道 |
| city | n. | 城市 |
| town | n. | 镇 |
| village | n. | 村庄 |
| country | n. | 国家 |
| world | n. | 世界 |
| school | n. | 学校 |
| hospital | n. | 医院 |
| shop | n. | 商店 |
| market | n. | 市场 |
| bank | n. | 银行 |
| station | n. | 车站 |
| hotel | n. | 旅馆 |
| restaurant | n. | 餐馆 |
| office | n. | 办公室 |
| factory | n. | 工厂 |
| farm | n. | 农场 |
| park | n. | 公园 |
| library | n. | 图书馆 |
| museum | n. | 博物馆 |
| bridge | n. | 桥 |
| corner | n. | 角落 |
| top | n. | 顶部 |
| bottom | n. | 底部 |
| side | n. | 侧面 |
| middle | n. | 中间 |
| left | n./adj. | 左边 |
| right² | n./adj. | 右边 |
| north | n. | 北 |
| south | n. | 南 |
| east | n. | 东 |
| west | n. | 西 |

### 4.8 物品与工具

| 词 | 词性 | 义项 |
|---|---|---|
| thing | n. | 东西；事情 |
| tool | n. | 工具 |
| machine | n. | 机器 |
| box | n. | 盒子 |
| bag | n. | 袋子 |
| bottle | n. | 瓶子 |
| cup | n. | 杯子 |
| plate | n. | 盘子 |
| bowl | n. | 碗 |
| knife | n. | 刀 |
| spoon | n. | 勺子 |
| key | n. | 钥匙 |
| lock | n. | 锁 |
| map | n. | 地图 |
| book | n. | 书 |
| paper | n. | 纸 |
| pen | n. | 笔（借词，暂留） |
| letter¹ | n. | 信 |
| letter² | n. | 字母 |
| picture | n. | 图画；照片 |
| clock | n. | 钟 |
| watch¹ | n. | 手表 |
| lamp | n. | 灯 |
| table | n. | 桌子 |
| chair | n. | 椅子 |
| bed | n. | 床 |
| ball | n. | 球 |
| game | n. | 游戏 |
| toy | n. | 玩具 |
| money | n. | 钱 |
| coin | n. | 硬币 |
| ticket | n. | 票 |
| gun | n. | 枪 |
| rope | n. | 绳子 |
| stick | n. | 棍子 |

### 4.9 交通

| 词 | 词性 | 义项 |
|---|---|---|
| car | n. | 汽车 |
| bus | n. | 公共汽车 |
| train | n. | 火车 |
| plane | n. | 飞机 |
| ship | n. | 船 |
| bike | n. | 自行车 |
| wheel | n. | 轮子 |

### 4.10 衣物

| 词 | 词性 | 义项 |
|---|---|---|
| clothes | n. | 衣服（整体，复数） |
| cloth | n. | 布 |
| shirt | n. | 衬衫 |
| coat | n. | 外套 |
| shoe | n. | 鞋 |
| hat | n. | 帽子 |
| dress | n. | 连衣裙 |
| pocket | n. | 口袋 |

---

### 4.11 抽象

| 词 | 词性 | 义项 |
|---|---|---|
| name | n. | 名字 |
| word | n. | 词 |
| sentence | n. | 句子 |
| language | n. | 语言 |
| number | n. | 数字 |
| color | n. | 颜色 |
| sound | n. | 声音 |
| music | n. | 音乐 |
| song | n. | 歌 |
| story | n. | 故事 |
| question | n. | 问题（提问） |
| answer | n. | 答案 |
| problem | n. | 难题 |
| idea | n. | 想法 |
| thought | n. | 思想 |
| dream | n. | 梦 |
| hope¹ | n. | 希望 |
| fear¹ | n. | 恐惧 |
| love¹ | n. | 爱 |
| hate¹ | n. | 恨 |
| anger | n. | 愤怒 |
| joy | n. | 快乐 |
| truth | n. | 真相 |
| lie² | n. | 谎言 |
| life | n. | 生命；生活 |
| death | n. | 死亡 |
| birth | n. | 出生 |
| health | n. | 健康 |
| sickness | n. | 疾病 |
| pain | n. | 疼痛 |
| work¹ | n. | 工作 |
| law | n. | 法律 |
| rule | n. | 规则 |
| right³ | n. | 权利 |
| power | n. | 力量；权力 |
| war | n. | 战争 |
| peace | n. | 和平 |
| group | n. | 群体 |
| team | n. | 队 |
| part | n. | 部分 |
| end | n. | 结尾 |
| start¹ | n. | 开始 |
| change¹ | n. | 变化 |
| help¹ | n. | 帮助 |
| need¹ | n. | 需要 |
| way | n. | 方法；路 |
| reason | n. | 原因 |
| result | n. | 结果 |
| chance | n. | 机会 |
| danger | n. | 危险 |
| secret | n. | 秘密 |
| news | n. | 消息 |
| message | n. | 信息；留言 |
| knowledge | n. | 知识 |
| science | n. | 科学 |
| art | n. | 艺术 |
| history | n. | 历史 |
| society | n. | 社会 |
| mind | n. | 心智 |
| memory | n. | 记忆 |
| choice | n. | 选择 |
| plan¹ | n. | 计划 |
| order¹ | n. | 命令 |
| order² | n. | 顺序 |
| size | n. | 大小 |
| weight | n. | 重量 |
| shape | n. | 形状 |
| line | n. | 线 |
| circle | n. | 圆 |
| point | n. | 点 |

> `government` 暂不入表，拟用 `ruling group` 生成；`information` 用 `news / knowledge` 分担。

### 4.12 颜色

| 词 | 词性 | 义项 |
|---|---|---|
| red | adj./n. | 红色 |
| blue | adj./n. | 蓝色 |
| green | adj./n. | 绿色 |
| yellow | adj./n. | 黄色 |
| black | adj./n. | 黑色 |
| white | adj./n. | 白色 |
| brown | adj./n. | 棕色 |
| gray | adj./n. | 灰色 |
| orange² | adj./n. | 橙色 |

### 4.13 材料

| 词 | 词性 | 义项 |
|---|---|---|
| wood | n. | 木头 |
| metal | n. | 金属 |
| glass¹ | n. | 玻璃 |
| iron | n. | 铁 |
| gold | n. | 金子 |
| silver | n. | 银子 |
| plastic | n. | 塑料 |
| cotton | n. | 棉花 |
| wool | n. | 羊毛 |

### 4.14 度量

| 词 | 词性 | 义项 |
|---|---|---|
| meter | n. | 米（长度单位） |
| gram | n. | 克 |
| liter | n. | 升 |
| degree | n. | 度 |
| dollar | n. | 元（货币单位） |
| cent | n. | 分（货币单位） |

> `kilometer / kilogram` 由 `thousand + meter / gram` 生成，不立条。

---

## 5. 动词

动词决定句子骨架。一条判据：**能用更简单的动词 + 介词/名词稳定替代的，不收**（如 `enter` 保留，`penetrate` 不收）。

### 5.1 基本动作与使役

| 词 | 词性 | 义项 |
|---|---|---|
| make | v. | 制造；使……（make him happy） |
| let | v. | 让；允许 |
| help² | v. | 帮助 |
| use | v. | 使用 |
| need² | v. | 需要 |
| want | v. | 想要 |
| get | v. | 得到 |
| give | v. | 给 |
| take | v. | 拿；取 |
| put | v. | 放 |
| keep | v. | 保留；保持 |
| hold | v. | 握住 |
| bring | v. | 带来 |
| send | v. | 送；寄 |
| carry | v. | 携带 |
| find | v. | 找到 |
| lose | v. | 丢失 |

### 5.2 位移与方位

| 词 | 词性 | 义项 |
|---|---|---|
| go | v. | 去 |
| come | v. | 来 |
| walk | v. | 走 |
| run | v. | 跑 |
| jump | v. | 跳 |
| swim | v. | 游泳 |
| fly | v. | 飞 |
| drive | v. | 驾驶 |
| ride | v. | 骑；乘坐 |
| move | v. | 移动 |
| turn | v. | 转 |
| fall | v. | 落下 |
| rise | v. | 升起 |
| stand | v. | 站 |
| sit | v. | 坐 |
| lie¹ | v. | 躺 |
| enter | v. | 进入 |
| leave | v. | 离开 |
| return | v. | 返回 |
| arrive | v. | 到达 |
| travel | v. | 旅行 |

### 5.3 感知

| 词 | 词性 | 义项 |
|---|---|---|
| see | v. | 看见（被动感知） |
| look | v. | 看（主动） |
| hear | v. | 听见 |
| listen | v. | 听（主动） |
| smell | v. | 闻 |
| taste | v. | 尝 |
| touch | v. | 触摸 |
| feel | v. | 感觉 |

### 5.4 言语

| 词 | 词性 | 义项 |
|---|---|---|
| say | v. | 说（内容） |
| tell | v. | 告诉 |
| speak | v. | 说话（语言能力） |
| talk | v. | 交谈 |
| ask | v. | 问 |
| answer | v. | 回答 |
| call¹ | v. | 叫；称呼 |
| call² | v. | 打电话 |
| read | v. | 读 |
| write | v. | 写 |
| sing | v. | 唱 |
| thank | v. | 感谢 |

### 5.5 思维与意愿

| 词 | 词性 | 义项 |
|---|---|---|
| know | v. | 知道 |
| think | v. | 想；认为 |
| remember | v. | 记得 |
| forget | v. | 忘记 |
| understand | v. | 理解 |
| believe | v. | 相信 |
| hope² | v. | 希望 |
| fear² | v. | 害怕 |
| worry | v. | 担心 |
| learn | v. | 学会 |
| teach | v. | 教 |
| study | v. | 学习；研究 |
| decide | v. | 决定 |
| choose | v. | 选择 |
| try | v. | 尝试 |
| plan² | v. | 计划 |
| mean | v. | 意思是 |

### 5.6 情感与表情

| 词 | 词性 | 义项 |
|---|---|---|
| like¹ | v. | 喜欢 |
| love² | v. | 爱 |
| hate² | v. | 恨 |
| smile | v. | 微笑 |
| laugh | v. | 笑（出声） |
| cry | v. | 哭 |

### 5.7 生活

| 词 | 词性 | 义项 |
|---|---|---|
| eat | v. | 吃 |
| drink | v. | 喝 |
| cook | v. | 煮；做饭 |
| wash | v. | 洗 |
| clean² | v. | 打扫 |
| sleep | v. | 睡 |
| wake | v. | 醒 |
| rest | v. | 休息 |
| live | v. | 生活；居住 |
| die | v. | 死 |
| grow | v. | 生长 |
| marry | v. | 结婚 |
| play | v. | 玩；演奏（play music） |
| work² | v. | 工作 |
| buy | v. | 买 |
| sell | v. | 卖 |
| pay | v. | 付钱 |
| cost | v. | 值（多少钱） |
| borrow | v. | 借入 |
| lend | v. | 借出 |
| own | v. | 拥有 |

### 5.8 变化与作用

| 词 | 词性 | 义项 |
|---|---|---|
| become | v. | 变成 |
| change² | v. | 改变 |
| open¹ | v. | 打开 |
| close¹ | v. | 关闭 |
| start² | v. | 开始 |
| stop | v. | 停止 |
| finish | v. | 完成 |
| continue | v. | 继续 |
| break | v. | 打破；弄坏 |
| fix | v. | 修理 |
| build | v. | 建造 |
| burn | v. | 燃烧 |
| melt | v. | 融化 |
| freeze | v. | 结冰 |
| cut | v. | 切 |
| hit | v. | 打；击 |
| kick | v. | 踢 |
| throw | v. | 扔 |
| catch | v. | 接住 |
| push | v. | 推 |
| pull | v. | 拉 |
| kill | v. | 杀 |
| fight | v. | 打斗；战斗 |
| win | v. | 赢 |

### 5.9 社会关系

| 词 | 词性 | 义项 |
|---|---|---|
| meet | v. | 遇见；会面 |
| join | v. | 加入 |
| wait | v. | 等待 |
| stay | v. | 停留；留下 |
| visit | v. | 拜访 |
| follow | v. | 跟随 |
| lead | v. | 带领 |

---

## 6. 形容词

形容词只收“不可由名词 + 介词短语稳定替代”的性质词；比较级、最高级由 `rules/05` 生成。

### 6.1 大小与形状

| 词 | 词性 | 义项 |
|---|---|---|
| big | adj. | 大的 |
| small | adj. | 小的 |
| long | adj. | 长的 |
| short | adj. | 短的 |
| tall | adj. | 高的（人、树） |
| high | adj. | 高的（位置、程度） |
| low | adj. | 低的 |
| wide | adj. | 宽的 |
| narrow | adj. | 窄的 |
| deep | adj. | 深的 |
| thick | adj. | 厚的 |
| thin | adj. | 薄的；瘦的 |
| round | adj. | 圆的 |
| flat | adj. | 平的 |
| straight | adj. | 直的 |

### 6.2 评价与性质

| 词 | 词性 | 义项 |
|---|---|---|
| good | adj. | 好的 |
| bad | adj. | 坏的 |
| right¹ | adj. | 正确的 |
| wrong | adj. | 错误的 |
| true | adj. | 真的 |
| false | adj. | 假的 |
| easy | adj. | 容易的 |
| hard¹ | adj. | 困难的 |
| important | adj. | 重要的 |
| possible | adj. | 可能的 |
| necessary | adj. | 必要的 |
| ready | adj. | 准备好的 |
| sure | adj. | 确定的 |
| safe | adj. | 安全的 |
| dangerous | adj. | 危险的 |
| free¹ | adj. | 自由的 |
| different | adj. | 不同的 |

### 6.3 物理属性

| 词 | 词性 | 义项 |
|---|---|---|
| hot | adj. | 热的 |
| cold | adj. | 冷的 |
| warm | adj. | 暖的 |
| cool | adj. | 凉的 |
| wet | adj. | 湿的 |
| dry | adj. | 干的 |
| clean¹ | adj. | 干净的 |
| dirty | adj. | 脏的 |
| heavy | adj. | 重的 |
| light² | adj. | 轻的 |
| fast | adj./adv. | 快的 |
| slow | adj. | 慢的 |
| strong | adj. | 强壮的 |
| weak | adj. | 虚弱的 |
| hard² | adj. | 坚硬的 |
| soft | adj. | 软的 |
| sharp | adj. | 锋利的 |
| dull | adj. | 钝的 |

### 6.4 感官

| 词 | 词性 | 义项 |
|---|---|---|
| bright | adj. | 明亮的 |
| dark | adj. | 暗的 |
| loud | adj. | 响的 |
| quiet | adj. | 安静的 |
| sweet | adj. | 甜的 |
| sour | adj. | 酸的 |
| bitter | adj. | 苦的 |
| salty | adj. | 咸的 |

### 6.5 情绪与性格

| 词 | 词性 | 义项 |
|---|---|---|
| happy | adj. | 快乐的 |
| sad | adj. | 悲伤的 |
| angry | adj. | 生气的 |
| afraid | adj. | 害怕的 |
| surprised | adj. | 惊讶的 |
| proud | adj. | 自豪的 |
| tired | adj. | 累的 |
| kind | adj. | 善良的 |
| beautiful | adj. | 美的 |
| ugly | adj. | 丑的 |

### 6.6 年龄与状态

| 词 | 词性 | 义项 |
|---|---|---|
| new | adj. | 新的 |
| old | adj. | 旧的；老的 |
| young | adj. | 年轻的 |
| rich | adj. | 富有的 |
| poor | adj. | 贫穷的 |
| full | adj. | 满的 |
| empty | adj. | 空的 |
| open² | adj. | 开着的 |
| busy | adj. | 忙的 |
| free² | adj. | 免费的 |
| sick | adj. | 生病的 |
| hungry | adj. | 饿的 |

### 6.7 时间与顺序

| 词 | 词性 | 义项 |
|---|---|---|
| late | adj. | 迟的 |
| early | adj. | 早的 |
| last | adj. | 最后的 |
| next | adj. | 下一个的 |

> `near` 已在 §2.4 以 `prep./adj.` 收录，不重复立条。

---

## 7. 副词

### 7.1 程度

| 词 | 词性 | 义项 |
|---|---|---|
| very | adv. | 很 |
| too¹ | adv. | 太 |
| so² | adv. | 这么；如此 |
| quite | adv. | 相当 |
| almost | adv. | 几乎 |
| only | adv. | 只 |
| just | adv. | 刚刚；就 |
| even | adv. | 甚至 |

### 7.2 时间

| 词 | 词性 | 义项 |
|---|---|---|
| now | adv. | 现在 |
| always | adv. | 总是 |
| often | adv. | 经常 |
| sometimes | adv. | 有时 |
| never | adv. | 从不 |
| ever | adv. | 曾经 |
| already | adv. | 已经 |
| still | adv. | 仍然 |
| yet | adv. | 还（未） |
| soon | adv. | 很快 |
| again | adv. | 再次 |

### 7.3 地点

| 词 | 词性 | 义项 |
|---|---|---|
| here | adv. | 这里 |
| there | adv. | 那里 |
| back² | adv. | 回（原处） |
| away | adv. | 离开 |
| together | adv. | 一起 |
| alone | adv. | 独自 |

### 7.4 方式

| 词 | 词性 | 义项 |
|---|---|---|
| well | adv. | 好地（good 的副词形式，不规则） |

> 其余方式副词一律由 `形容词 + -ly` 生成（slow → slowly），不立条。

### 7.5 语气

| 词 | 词性 | 义项 |
|---|---|---|
| maybe | adv. | 也许 |
| also | adv. | 也 |
| too² | adv. | 也（句末） |
| either | adv. | 也（否定句） |
| neither | adv. | 也不 |

---

## 8. 多义词登记

**规则**：不同义项必须分行立条（不同编号）；同一义项兼类可合并为一条。下表记录本表全部拆分，防止回改时被合并。

| 词形 | 义项 A | 义项 B | 义项 C | 处理 |
|---|---|---|---|---|
| light | light¹ 光（n.） | light² 轻（adj.） | — | 分行 |
| right | right¹ 正确（adj.） | right² 右边（n./adj.） | right³ 权利（n.） | 分行 |
| back | back¹ 背部（n.） | back² 回（adv.） | — | 分行 |
| hard | hard¹ 困难（adj.） | hard² 坚硬（adj.） | — | 分行 |
| free | free¹ 自由（adj.） | free² 免费（adj.） | — | 分行 |
| open | open¹ 打开（v.） | open² 开着的（adj.） | — | 分行 |
| glass | glass¹ 玻璃（n.） | 玻璃杯 | — | 只留 A，杯子用 cup |
| orange | orange¹ 橙子（n.） | orange² 橙色（adj.） | — | 分行 |
| no | no¹ 没有（det.） | no² 不（adv.） | — | 分行 |
| her | her¹ 她（pron.） | her² 她的（det.） | — | 分行 |
| that | that¹ 那个（det.） | that² 引导从句（conj.） | — | 分行 |
| order | order¹ 命令（n.） | order² 顺序（n.） | — | 分行 |
| letter | letter¹ 信（n.） | letter² 字母（n.） | — | 分行 |
| call | call¹ 叫（v.） | call² 打电话（v.） | — | 分行 |
| like | like¹ 喜欢（v.） | like² 像（prep.） | — | 分行 |
| lie | lie¹ 躺（v.） | lie² 谎言（n.） | 说谎 | 只留 A、B，说谎用 tell lie |
| watch | watch¹ 手表（n.） | 观看（v.） | — | 只留 A，观看用 look |
| close | close¹ 关（v.） | 近的（adj.） | — | 只留 A，近用 near |
| play | play 玩；演奏（v.） | — | — | 同一义项的两用法，合并 |
| before/after | 在……前/后 | — | — | 同一义项兼介词、连词、副词 |
| so | so¹ 所以（conj.） | so² 这么（adv.） | — | 分行 |
| work | work¹ 工作（n.） | work² 工作（v.） | — | 同义兼类，分列便于检索 |
| point | point 点（n.） | 指（v.） | — | 只留 A |
| second | second¹ 秒（n.） | 第二（num.） | — | 第二由数词规则生成 |

---

## 9. 待定与排除

### 9.1 明确排除

- 专有名词：人名、地名、国名、品牌名不入表，另建专名表。
- 缩写与符号：`TV`、`OK`（已入 okay）、单位符号等。

### 9.2 借词层（待决策）

`computer`、`phone`、`coffee`、`pizza`、`radio`、`internet` 这类词有两个方案：

1. **借词层**：承认它们不可分解，单列一张“技术借词表”，与基表隔离；
2. **构词**：`computer` = thinking machine、`phone` = far-speak machine、`internet` = world net。

建议先用方案 1 保证可用，再逐步用方案 2 替换，并把替换结果记入映射表。

### 9.3 待验证的组合方案

| 对象 | 拟用方案 | 风险 |
|---|---|---|
| 11–99 数词 | `two-ten`、`three-ten-five` | 与基数词读音差异大，需母语者可读性测试 |
| 序数 | one-th、two-th；first/second/third 不规则 | 不规则项须硬编码 |
| 星期 | `day one` … `day seven` | 与“第一天”歧义 |
| 月份 | `month one` … `month twelve` | 同上 |
| 今天/明天/昨天 | `this day / next day / last day` | 与“下一天”歧义 |

### 9.4 待补规则

- 派生：`-er`（做……的人）、`-ly`（……地）、`-less`（没有……的）、`un-`（不……）、`re-`（再……）。
- 不规则屈折清单：people、teeth、feet、mice、leaves、men、women、children。
- 复合词长度上限（建议 ≤ 3 个基词），超出改用 `of / for` 短语，避免名词串歧义。

---

## 10. 统计

| 类别 | 词条数 |
|---|---|
| 功能词 | 108 |
| 逻辑词 | 26 |
| 名词 | 320 |
| 动词 | 133 |
| 形容词 | 84 |
| 副词 | 31 |
| **合计** | **702** |

### 10.1 与旧版对比

旧版 138 词（名词 52 / 动词 35 / 形容词 37 / 逻辑词 14），无功能词、无多义拆分、无编号约定。本版补齐功能词与缺失语义场，并按义项拆分。

### 10.2 下一步

1. 补齐 `rules/` 六条规则的正文与反例。
2. 建立“标准英语 → 简化英语”映射表，用牛津 3000 跑覆盖率。
3. 逐词补英文释义，做循环性检查（定义中不得出现被定义词及其派生）。

