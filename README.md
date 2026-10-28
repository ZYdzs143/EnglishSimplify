# EnglishSimplify · 英语简化计划

用“基”的思想重构英语词表：先确定一组不可再分解的基本词，其余词汇全部由基本词按规则组合生成。

```
pork      →  pig meat
beef      →  cow meat
chicken   →  chicken meat
mutton    →  sheep meat
```

与中文“猪 + 肉 = 猪肉”的构词方式一致：不背新词，只学组合。

派生同样只有一条规则，没有例外：

```
person → persones      child → childes      mouse → mouses
good   → gooder        well  → goodly       first → oneth
```

## 三条设计原则

| 原则 | 含义 | 验证方式 |
|---|---|---|
| 无关性 | 基本词之间不能互相定义，否则循环 | 一词一义、近义词只留一个、派生词不入表 |
| 张成性 | 目标词表中的每个词都能被分解 | 用牛津 3000 / COCA 5000 跑覆盖率 |
| 唯一性 | 每个概念只有一种规范写法 | 组合规则必须确定，禁止同义变体 |

唯一性最容易被忽略：若 `pork` 可以写成 `pig meat` / `meat of pig` / `pig's meat`，这套语言就退化成方言，既教不会人，也无法让程序互转。

## 目录

```
core-word/
  index.md        基表：701 个词条，按功能词、逻辑词、名词、动词、形容词、副词分类
rules/
  04-plural.md    复数规则：统一 +es，零词法例外
  examples/       组合示例（待建）
```

## 当前进度

- [x] 基表 v2.0：701 词条，含功能词、多义词按义项拆分、不可分解性约定
- [x] 复数规则：一条规则、零例外（`rules/04-plural.md`）
- [ ] 其余五条规则正文与反例
- [ ] 标准英语 → 简化英语映射表
- [ ] 覆盖率校验脚本

基表入口：[core-word/index.md](./core-word/index.md) · 复数规则：[rules/04-plural.md](./rules/04-plural.md)
