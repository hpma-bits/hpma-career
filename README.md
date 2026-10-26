# hpma-career

hpma-career-data：职业数据包（草药学家 + 烹饪艺术家），包含收购/购入目录、配方与炊具、职业等级、商店等级与职业研究技能树，中英双语（zh/en）。

| 数据 | 条数 | 说明 |
|---|---|---|
| 植物 | 29 | 4 品质档，含稀有色价 |
| 料理 | 45 | 159 个物品按名称归并（`item_ids`） |
| 种子 | 29 | 与植物一一对应 |
| 材料 | 43 | 商店 39 + 植物源 4 |
| 配方 | 44 | 灶台 22 / 甜品台 22 |
| 炊具 | 6 | 显示名未提供（见下） |
| 商店等级 | 6 | 高价收购倍率/件数/预算 |
| 职业等级 | 36 | 2 职业 × 18 级 |
| 研究技能 | 101 | `type/sub_type/param` 原样保留 |

## 目录结构

```
hpma-career/
├── README.md          # 本文件
├── LICENSE-NOTES.md   # 使用与许可说明
├── manifest.json      # 版本、counts、coverage、notes（数据契约细节以 notes 为准）
├── career.json        # 全部数据（单文件）
├── check.html         # 核对页：浏览器打开，数据内嵌，逐条勾选
├── images/            # 图标 PNG（含 4 张品质光环）
├── images_webp/       # 图标 WebP 副本（q82，优先加载，失败回退 PNG）
└── schema/            # JSON Schema（career + manifest）
```

## 版本轴

tag 与发布均为 `career-v{S}.{D}.0`：`S` = schema_version（数据结构变更才 +1），`D` = data_version（内容刷新，YYYYMMDD）。

## 消费口径（必读）

- **币种按 (条目, 档位) 独立**：存在低档金币、绽放档宝石的混币种植物，不要按条目假定单一币种。
- **price 是基础价**。商店等级带来的是高价收购通道：`shop_levels[].hva_rate` 为额外倍率（1/2/3 = +100/200/300%），`hva_slots` 为每周件数，`hva_budget` 为每周预算区间。菜品售价天赋见 `research`（sub_type 25/26，`param` = [每份研究 +X%, 上限 Y%]）。
- **`duration_ms` 是毫秒，÷1000 = 秒**（不是分钟）。
- **`buy_limit` 99 是游戏真上限**，不是"无限"哨兵。
- **稀有色是运行时着色**（11 种观赏色），没有独立变体图片；`price_rare_color > price` 表示该档有稀有色溢价，相等表示无溢价。
- **炊具显示名未提供**：`utensils[].i18n.zh/en.name` 为 null，`name_key` 仅作标识，消费端自行命名。
- 材料获取通道恰一：`shop`（商店购入）/ `plant`（植物自种，链回植物绽放档）。
- 图标按文件名去重；缺失图标计入 `manifest.coverage.missing_icons`。

## 免责

仅供个人学习研究，请勿商用或再分发素材。如有权利方异议，请联系删除。
