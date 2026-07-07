# 附錄 D. R&D 文件命名與 Frontmatter 標準

> 公司專案A的 R&D 文件命名與 frontmatter 標準(`_NAMING_FRONTMATTER_STANDARD`)的通用化版本。

---

## D.1 命名標準

### D.1.1 atom

```
<category>_<topic>_<subtopic>.md

示例:
combat_global_cooldown_constant.md
narrative_voice_profile_K_007.md
ui_button_primary_style.md
```

snake_case。類別字首。

### D.1.2 決策卡

```
D<YEAR>_Q<QUARTER>_<NUMBER>.md

示例:
D2026_Q2_017.md
```

年份、季度、編號。

### D.1.3 會議記錄

```
<category>_<YYYY-MM-DD>[_<seq>].md

示例:
95_BattleTF_2026-05-18.md
art_review_2026-05-18_1.md
art_review_2026-05-18_2.md
```

### D.1.4 規格書

```
spec_<topic>.md

示例:
spec_combat_global_cooldown.md
spec_guild_attendance.md
```

### D.1.5 報告

```
report_<period>_<type>.md

示例:
report_W21_alpha_gap.md
report_Q2_user_voice.md
```

---

## D.2 Frontmatter 標準

### D.2.1 atom

```yaml
---
name: combat_global_cooldown_constant
description: 定義戰鬥系統的全域性冷卻標準值
type: atom
category: combat
status: active
priority: P0
related_atoms:
  - combat_skill_cooldown_rule
  - combat_healing_skill_cooldown_exception
created: 2026-05-18
last_modified: 2026-05-18
related:
  derives_from: [combat_design_principle]
  affects: [combat_skill_cooldown_rule, ui_skill_cooldown_indicator]
---
```

### D.2.2 決策卡

```yaml
---
decision_id: D2026_Q2_017
title: 戰鬥全域性冷卻統一為 0.5 秒
type: system_change
status: active
created: 2026-05-18
created_by: 團隊成員 A
approved_by: 李旼洙
scope:
  - combat_system
affected_atoms: [...]
implementation:
  target_build: 2026-05-18
verification:
  layer_1: passed
  layer_2: passed
  layer_3: pending
---
```

### D.2.3 會議記錄

```yaml
---
type: meeting_note
category: battle
date: 2026-05-18
attendees: [團隊成員 A, 團隊成員 B, 李旼洙]
related_atoms: [...]
---
```

### D.2.4 規格書

```yaml
---
title: 公會簽到功能規格
type: spec
priority: P1
target_milestone: MS2
---
```

---

## D.3 必填 vs 選填欄位

### D.3.1 必填欄位

| 文件型別 | 必填 |
|---|---|
| atom | name, description, type, category, status |
| 決策卡 | decision_id, title, type, status, created, scope |
| 會議記錄 | type, category, date, attendees |
| 規格書 | title, type, priority |

### D.3.2 選填欄位（有則更好）

| 文件型別 | 選填 |
|---|---|
| atom | related, last_modified, priority |
| 決策卡 | rationale, related_decisions, verification |
| 會議記錄 | related_atoms, sub_topic |
| 規格書 | target_milestone, related_atoms |

---

## D.4 Lint 自動檢查

```bash
# frontmatter_lint.py

for file in glob("**/*.md"):
    fm = parse_frontmatter(file)
    if not fm:
        warn(f"{file}: 缺少 frontmatter")
    
    doc_type = infer_type_from_filename(file)
    required = REQUIRED_FIELDS[doc_type]
    
    for field in required:
        if field not in fm:
            warn(f"{file}: 缺少必填欄位 {field}")
```

構建時自動執行。違規觸發 alert。

---

## D.5 防止命名衝突

| 領域 | 防止 |
|---|---|
| atom name | 全域性 unique |
| 決策 ID | 季度內 unique |
| 會議 ID | 日期 + seq |
| 檔名 | 資料夾內 unique |

命名衝突時自動阻止。

---

## D.6 變更流程

### D.6.1 atom 重新命名

```
1. 建立新名稱的 atom
2. 將原 atom 的所有 wikilink 更新為新名稱(自動)
3. 將原 atom 棄用(deprecated)+ 重定向(redirect)
4. 1 個月後移至 _archive
```

倉促的重新命名有損壞資料的風險。

### D.6.2 frontmatter 標準變更

```
1. 提出變更理由(decision 流程)
2. 為所有現有文件編寫遷移指令碼
3. 更新構建 lint
4. 通知團隊
```

---

## D.7 讀者參考

本標準基於作者的環境。讀者需根據自身環境進行調整。核心在於:

| 核心 | 理由 |
|---|---|
| 命名一致性 | 檢索、自動化 |
| Frontmatter 標準 | 工具友好 |
| 必填、選填分離 | 填寫負擔 ↓ |
| Lint 自動 | 強制標準 |
| 變更流程 | 保護資料 |
