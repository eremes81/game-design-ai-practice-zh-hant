---
title: "5.1 NarrativeDocs Layer 0~4 結構"
part: 5
chapter: 1
status: v3
version: v3
written: 2026-05-24
author: 李旼洙
ip_check: done
---

# 5.1 NarrativeDocs Layer 0\~4 結構

走進會議室,白板上有一個角色名字被紅筆圈了起來。是個叫金某的 NPC。在一位策劃的支線任務裡,他是"在主角小時候收養並把他養大的養父";而在另一位策劃的主線任務第 3 章裡,他卻是"背叛主角後離去的舊日同伴"。兩份文件都在一個月前通過了審批,兩者都已進入了構建。連配音錄製的報價都拿到了。

誰都沒有錯。兩位策劃都讀過世界觀文件,也都參考了角色設定。問題在於,同一個角色的設定散落在三個不同的檔案裡,而其中哪一個才是"真的",誰也無法斷言。世界觀文件是一整塊 70 頁的 Word 檔案,一搜索,金某出現在十一個地方。哪一行是決定、哪一行是備註,沒有任何區分。

那天會議結束後定下來的事情,就是把 NarrativeDocs 拆成五層。本章講的就是這五層的故事。

---

## 5.1.1 為什麼從最抽象的領域開始

把按領域的 Layer 分解先從敘事開始,是有理由的。

敘事最抽象。世界觀、情感、基調這類東西落不到數字上。它不像美術或系統那樣有"精靈圖數量""傷害係數"這種明確的單位。如果連這樣抽象的領域都能被幹淨地分解為 Layer,那麼更具體的其他領域自然會用同樣的模式解開。這相當於先看難的地方能不能走通。

再者,敘事的介面最多。角色與美術相接,任務與內容、關卡相接,臺詞與 UX、本地化相接,獎勵與系統相接。它處在橫跨領域最多的位置,所以 Layer 統合的價值會立刻顯現出來。

最後,自然語言產出物的佔比最高。因此它也是 AI 輔助作用最大的領域。不過並非所有遊戲都以敘事為中心。如果是休閒、街機型別,本章的深度可能會顯得過頭。即便如此,"把一整塊文件拆成 Layer、收窄介面"這一骨架本身,可以原封不動地搬到任何領域。

---

## 5.1.2 五格抽屜

把 NarrativeDocs 分解為五層後的樣子如下。願景(L0)在上,構建·QA(L4)在下,連線各層之間的通道有意收得很窄。

<svg viewBox="0 0 720 520" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif">
  <style>
    .layerbox { rx: 8; }
    .ltitle { font-size: 15px; font-weight: bold; fill: #1a1a2e; }
    .ldesc { font-size: 11px; fill: #444; }
    .iface { font-size: 11px; fill: #b03030; font-style: italic; }
    .owner { font-size: 10px; fill: #2a6; }
  </style>

  <!-- L0 -->
  <rect x="120" y="20" width="480" height="60" rx="8" fill="#fdeaea" stroke="#c0392b" stroke-width="2"/>
  <text x="140" y="44" class="ltitle">L0 願景 —— "這個世界是什麼"</text>
  <text x="140" y="64" class="ldesc">world_premise · narrative_pillar · tone_manifesto  (不變 · 約 4.5 頁)</text>
  <text x="560" y="44" class="owner" text-anchor="end">總監·主策</text>

  <!-- arrow L0->L1 -->
  <line x1="360" y1="80" x2="360" y2="108" stroke="#888" stroke-width="2"/>
  <polygon points="360,116 355,106 365,106" fill="#888"/>
  <text x="372" y="100" class="iface">pillar · tone (變更時 L1 重新審查)</text>

  <!-- L1 -->
  <rect x="120" y="116" width="480" height="60" rx="8" fill="#eef2fb" stroke="#2c5fa0" stroke-width="2"/>
  <text x="140" y="140" class="ltitle">L1 系統 —— "如何運作"</text>
  <text x="140" y="160" class="ldesc">faction_system · reputation_model · dialogue_branching_rule · lore_consistency_rule</text>
  <text x="560" y="140" class="owner" text-anchor="end">資深敘事</text>

  <!-- arrow L1->L2 -->
  <line x1="360" y1="176" x2="360" y2="204" stroke="#888" stroke-width="2"/>
  <polygon points="360,212 355,202 365,202" fill="#888"/>
  <text x="372" y="196" class="iface">規則手冊·分支策略 (受影響任務自動列表化)</text>

  <!-- L2 -->
  <rect x="120" y="212" width="480" height="60" rx="8" fill="#eef9ee" stroke="#2e8b57" stroke-width="2"/>
  <text x="140" y="236" class="ltitle">L2 內容 —— "發生了什麼"</text>
  <text x="140" y="256" class="ldesc">main_quest · side_quest · character_bible · lore_codex  (最厚的一層)</text>
  <text x="560" y="236" class="owner" text-anchor="end">多名策劃</text>

  <!-- arrow L2->L3 (narrow!) -->
  <line x1="360" y1="272" x2="360" y2="300" stroke="#b03030" stroke-width="3"/>
  <polygon points="360,308 354,297 366,297" fill="#b03030"/>
  <text x="372" y="292" class="iface">quest_id · npc_id · dialogue_id (僅一列)</text>

  <!-- L3 -->
  <rect x="120" y="308" width="480" height="60" rx="8" fill="#fbf5e9" stroke="#c08a2c" stroke-width="2"/>
  <text x="140" y="332" class="ltitle">L3 資料 —— "機器讀取的形態"</text>
  <text x="140" y="352" class="ldesc">quest_table · npc_table · dialogue_id_table · reward_table  (自然語言 0 行)</text>
  <text x="560" y="332" class="owner" text-anchor="end">敘事+資料</text>

  <!-- arrow L3->L4 -->
  <line x1="360" y1="368" x2="360" y2="396" stroke="#888" stroke-width="2"/>
  <polygon points="360,404 355,394 365,394" fill="#888"/>
  <text x="372" y="388" class="iface">表格變更時自動觸發 lint</text>

  <!-- L4 -->
  <rect x="120" y="404" width="480" height="60" rx="8" fill="#f2eefb" stroke="#7a4fa0" stroke-width="2"/>
  <text x="140" y="428" class="ltitle">L4 構建·QA —— "能否上線"</text>
  <text x="140" y="448" class="ldesc">narrative_qa_checklist · voice_review_log · localization_status</text>
  <text x="560" y="428" class="owner" text-anchor="end">敘事+QA</text>

  <!-- side note: locked anchor -->
  <line x1="120" y1="50" x2="60" y2="50" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="50" x2="60" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="434" x2="120" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <text x="52" y="245" class="iface" text-anchor="middle" transform="rotate(-90 52 245)">L0 每次都作為上下文注入 (生成·驗收的錨點)</text>
</svg>

落到資料夾上就是下面這個形態。每個檔名都不是書中抽象出來的名字,而是實際存在於那個資料夾中的檔名。

```
NarrativeDocs/
├── Layer0_Vision/
│   ├── world_premise.md          (世界觀前提 —— 不變)
│   ├── narrative_pillar.md       (情感支柱 3 根)
│   └── tone_manifesto.md         (基調·禁忌用語清單)
├── Layer1_System/
│   ├── faction_system.md
│   ├── reputation_model.md
│   ├── dialogue_branching_rule.md
│   └── lore_consistency_rule.md
├── Layer2_Content/
│   ├── main_quest/               (以章為單位)
│   ├── side_quest/
│   ├── character_bible/
│   └── lore_codex/
├── Layer3_Data/
│   ├── quest_table.xlsx
│   ├── npc_table.xlsx
│   ├── dialogue_id_table.xlsx
│   └── reward_table.xlsx
└── Layer4_Build_QA/
    ├── narrative_qa_checklist.md
    ├── voice_review_log.md
    └── localization_status.md
```

重要的一點是,這五層不由一個人負責。每一層的主負責人各不相同,只把相鄰兩層之間的通道標準化。上圖中的紅色箭頭就是那條通道。尤其是 L2 與 L3 之間的通道,故意畫得最窄(粗紅箭頭),其中的理由後面再看。

用抽屜來比喻,就是一個五格抽屜。第一格里放絕不挪動的世界觀一行,第二格里放規則手冊,第三格里放正文,第四格里放表格,第五格里放驗收日誌。格與格之間的通道很窄,通道之上掛著變更通知的鈴鐺。

---

## 5.1.3 L0 —— 為了讓它不變而寫得儘量小

L0 不會變。它一變,遊戲的身份認同就變了。所以篇幅必須小。小才不會變。

| 文件 | 篇幅 |
|---|---|
| world_premise.md | A4 1.5 頁 |
| narrative_pillar.md | A4 1 頁 (情感 3 個) |
| tone_manifesto.md | A4 2 頁 (基調 + 禁忌用語清單) |

合起來約 4.5 頁。這就是 L0 的分量。一旦變重,人們就會害怕變更;一害怕,其他層就開始繞過 L0。繞行一旦開始,L0 就成了一份死文件。

`narrative_pillar.md` 的實際骨架是下面這個樣子(內容已抽象化)。

```markdown
---
title: 敘事情感支柱
layer: L0
status: locked
last_updated: 2026-05-18
---

## 1. 對失去之物的懷念
- 玩家在每一章結尾都會失去一樣東西。
- 失去的東西不會再回來 (只能通過回想)。

## 2. 義務與自由的衝突
- 所有主要 NPC 都揹負著兩種義務。
- 玩家的選擇只能保全其中一種義務。

## 3. 微小舉動的分量
- 比起宏大的英雄行為,微小的善意會帶來更大的結果。
```

這三行支柱,決定了它下面數百頁的方向。`status: locked` 不只是一個普通標籤。L4 的自動檢查之一會讀取這個標籤,使得 locked 文件在 PR 中被修改時,若沒有主敘事的批准就無法合併。

---

## 5.1.4 L1 —— 與程式碼最接近的敘事

L1 可以變更,但成本很大。因為它是規則手冊。規則手冊改一行,所有遵循該規則的內容都會受到影響。

`faction_system.md` 的骨架如下。

```markdown
---
title: 勢力系統
layer: L1
atoms:
  - faction_relation_matrix
  - faction_membership_rule
  - faction_quest_eligibility
---

## 1. 勢力概念
N 個勢力。每個勢力由 (理念、資源、領土) 定義。

## 2. 勢力之間的關係
- relation_matrix.json (-3 敵對 ~ +3 同盟)
- 關係變化觸發條件: 主線任務決定、聲望臨界

## 3. 玩家歸屬規則
- 同時歸屬最多 2 個 (敵對關係不可同時歸屬)
- 退出懲罰: 聲望 -2,同盟勢力 -1
```

請留意 frontmatter 的 `atoms:` 列表。這三個 atom 名稱不是普通的備註,而是第 7 部分本體論與第 11 部分關係圖所追蹤的識別符號。當某個任務引用了 `faction_quest_eligibility`,這條規則一旦變更,該任務就會自動出現在受影響列表裡。L1 是與遊戲程式碼最接近的敘事產出物,所以要與系統策劃結對作業。

---

## 5.1.5 L2 —— 最厚的一層,正文居住的地方

L2 最厚。主線任務、支線任務、角色聖經、傳說辭典全都住在這裡。先前在會議室裡衝突過的"養父 vs 背叛的同伴"金某的真正設定,如今也只以 `character_bible/` 中的一個檔案存在。那個檔案是單一真相來源,任務只引用它。

主線任務資料夾是下面這個形態。

```
main_quest/
├── chapter_01_awakening/
│   ├── 00_chapter_overview.md
│   ├── 01_quest_a_call_to_arms.md
│   ├── 02_quest_b_first_choice.md
│   └── ...
├── chapter_02_road/
│   └── ...
└── _TEMPLATES/
    └── quest_template.md
```

每個任務檔案都遵循 atom 標準格式。

```markdown
---
title: 拿起武器時
layer: L2
type: main_quest
atoms:
  - quest_chapter_01_awakening_a
related:
  affects: [reputation_model, faction_relation_matrix]
  derives_from: [narrative_pillar, world_premise]
  requires: [character_kim, faction_alpha]
  part_of: chapter_01_awakening
---

## 進行階段
1. ...

## 分支
- 選擇 A 方案時: ...
- 選擇 B 方案時: ...

## 獎勵 (參見 L3)
- reward_table.xlsx → quest_001 行
```

核心是 `related:` 塊。在寫下 `requires: [character_kim]` 的那一刻,這個任務就聲明瞭它從 character_bible 取用金某的設定,不再在自己的檔案裡重新定義金某。敘事正文放在 L2,數值獎勵放在 L3 表格。兩者若放在同一個檔案裡,每改一行表格都得動到正文,而那樣一來翻譯鍵就會錯位。

---

## 5.1.6 L3 —— 沒有一行自然語言的層

L3 是表格和 ID。一行自然語言句子都進不來。

```
quest_table.xlsx
| quest_id | chapter | type | unlock_level | reward_xp | reward_gold | dialogue_set_id |
|----------|---------|------|--------------|-----------|-------------|-----------------|
| q_001    | ch01    | main | 1            | 500       | 100         | ds_001          |
| q_002    | ch01    | main | 2            | 800       | 150         | ds_002          |
```

連臺詞也只用 ID 來引用。正文另放在 `dialogue_id_table.xlsx` 裡,與翻譯鍵 1:1 對映。連線 L2 與 L3 的通道,只需 `quest_id` 一列就夠了。前圖中唯獨這條通道是粗紅箭頭,原因正在於此。把介面收窄到一列,是 Layer 分離的核心。通道一寬,兩側就會對彼此知道得太多,改動一側時另一側就會跟著崩壞。

---

## 5.1.7 L4 —— 出貨關卡

L4 是驗收與出貨。每當新內容進來,自動·人工檢查就會啟動。自動檢查由指令碼來跑。下面這四個是實際掛在 CI 上的 lint。

| 檢查 | 工具 |
|---|---|
| 所有 dialogue_id 對映存在 | `dialogue_lint.py` |
| 所有 quest_id 都屬於某個 chapter | `quest_lint.py` |
| 獎勵合計在各章曲線範圍之內 | `reward_curve_check.py` |
| 禁忌用語是否出現 | `tone_lint.py` (基於 L0 tone_manifesto) |

請注意 `tone_lint.py` 直接讀取 L0 的 `tone_manifesto.md` 這一點。最上層(不變的願景)與最下層(出貨關卡)通過自動化直接連線在了一起。願景裡寫下的禁忌用語,若在上線前夕從正文中被檢出,構建就會被攔下。

自動抓不到的東西,由人來看。

| 檢查 | 負責 |
|---|---|
| 與 L0 情感支柱契合 | 主敘事 |
| 角色配音一致性 | 角色負責人 + 敘事 |
| 本地化可行性 | 本地化人員 |

自動與人工的邊界一旦清晰,驗收時間就會變得可預測。"這一章的驗收要幾天?"也就能答得上來了。

---

## 5.1.8 讓 AI 來做 Layer —— 實操記錄

到這裡為止是結構。然而這個結構真正發揮作用的地方,是在製作新內容時。在一個已經鋪好五層的專案裡,接到一條支線任務的一句話想法,把它撒進各 Layer 的工作,我讓 Claude 做了一遍,這裡原樣搬出那次真實的會話(實操記錄,worked transcript —— 完整保留的真實操作過程記錄)。不做摘要,連偏掉的部分和被拒絕的部分都一併收錄。

**發出的提示詞(全文):**

```
絕對不要違反附上的 L0/L1 上下文,按我們的 Layer 結構來分解。

[narrative_pillar.md 全文 —— 情感支柱 3 個]
[tone_manifesto.md 節選 —— 禁忌用語: "命運"、"預言"、"被選中的人"]
[character_bible/character_kim.md 節選 —— 金: 收養主角的養父,
 寡言,話尾含糊,不直接說出情感]

想法: "金把亡妻的遺物交給玩家的一段簡短支線任務。"

L2 任務檔案(含 related 塊,正文 200 字左右)、L3 quest_table 行和
dialogue_id,還有 tone 違規的自我檢查。先只寫 L2 然後停下。
```

**Claude 的原始輸出(L2):**

```markdown
---
title: 褪色的手帕
layer: L2
type: side_quest
atoms:
  - quest_side_kim_keepsake
related:
  affects: [reputation_model]
  derives_from: [narrative_pillar]
  requires: [character_kim]
  part_of: chapter_02_road
---

## 進行階段
1. 金悄悄把玩家叫過來。不像平常那樣直接說出來意。
2. 遞出一塊舊手帕。"這個……還是你拿著比較好。"
3. 玩家若問那是什麼,金不作答,轉頭望向窗外。
4. (選擇) 接下 / 婉拒。

## 分支
- 接下: 金的聲望 +1。之後的章節中解鎖 1 次與手帕相關的回想。
- 婉拒: 金點點頭,把手帕重新收起。聲望無變化。
  手帕永遠不再出現。

## 獎勵 (參見 L3)
- reward_table.xlsx → quest_side_kim_keepsake 行
```

到這裡 Claude 停了下來,並補上了一行。

> "為了體現 L0 支柱第 1 條(失去的東西不會再回來),我讓選擇'婉拒'時手帕永遠消失。不過有一點需要確認。亡妻的設定在 character_kim.md 節選裡並不存在。這是我擅自加進去的,可能會與角色聖經衝突。"

**人的驗證與拒絕:**

這段輸出的基調很準。金的寡言、話尾含糊、不直接說出情感的習慣,都活了下來。也沒有禁忌用語。然而最後那條自我檢查恰恰點中了真正的問題。金有一位亡妻的設定,哪裡都沒有。AI 從"遺物"這個詞自然地推斷出了已故的配偶,但這是在角色聖經裡偷偷加入新事實的行為。這正是本章開頭會議室裡那起事故的種子。

所以我拒絕了。發回了重新請求。

**重新請求:**

```
基調不錯。但"亡妻"是聖經裡沒有的新設定,不能用。
金的過去只確定到"離開故鄉時留下了點東西"為止。不要指定
遺物的具體身份,只含糊地改成"很久以前留下的東西"之類。
手帕也是聖經裡沒有的,所以降到"一塊布片"之類。
```

**重新請求後的輸出(節選):**

```
2. 遞出一塊舊布片。"很久以前……我留下了一樣東西。
   這個就當是它的一角吧。"
3. 玩家若問那是什麼,金不作答,轉頭望向窗外。
```

這次就接受了。既沒有把金的過去重新釘死,又觸及了情感支柱第 1 條(失去)。失去的究竟是什麼,直到最後都含糊地留著。

這一次會話呈現出來的有兩點。第一,只要把 Layer 上下文(L0 支柱 + L1 基調 + L2 聖經)準確注入,AI 就能把基調對得驚人地好。第二,AI 一遇到空白就會煞有介事地填滿。當那個填補是聖經裡沒有的新事即時,抓住它的依然是人。Layer 結構的 `requires: [character_kim]` 告訴了我們"該去看哪裡",所以驗證者立刻就知道該和哪個檔案對照。要是沒有結構,就得把 70 頁重新翻一遍。

---

## 5.1.9 窄通道之上的通知鈴

把五層分開的真正理由,是為了收窄介面。而每一處窄介面都貼上變更檢測的自動化。

| 介面 | 流動的是什麼 |
|---|---|
| L0 → L1 | pillar、tone (變更時觸發 L1 規則手冊重新審查) |
| L1 → L2 | 規則手冊·分支策略 (變更時受影響任務自動列表化) |
| L2 → L3 | quest_id、npc_id、dialogue_id (僅一列) |
| L3 → L4 | 表格變更時自動觸發 lint |

例如在 L1 的 `faction_system.md` 中,把"同時歸屬最多 2 個"改成"最多 1 個"的 PR 提上去時,關係圖會掃過引用了 `faction_quest_eligibility` 的 L2 任務,生成一份受影響列表,並把這份列表自動附加到 PR 評論裡。改規則的人不必"約兩三次會去查誰受影響",看著評論裡附的列表,開個 30 分鐘的會就結束了。

核心是這一點。如果只分 Layer 而介面含糊,那就只是隔板多了幾塊而已。比起 Layer 分離本身,介面的自動化才是本質。

---

## 5.1.10 運營 6 個月,改變了什麼

遷移到五層、執行 6 個月之後的測量結果。下面的數值基於作者團隊的運營記錄,但絕對值只以方向·比率來呈現(作者估算·未經驗證)。分離前是憑記憶,分離後是實測,因此並非把同一份資料量了兩次,這是一個侷限。

| 專案 | Layer 分離前 | Layer 分離後 |
|---|---|---|
| 新策劃入職上手 | 3 周 | 1 周 |
| 規則手冊變更影響範圍掌握 | 開會 2\~3 次 | 自動評論 + 會議 30 分鐘 |
| 製作一章新主線任務 | 4 周 | 2.5 周 |
| 上線前一章驗收 | 5 天 | 2 天 |
| 本地化遺漏事故 | 每季度 3\~5 件 | 每季度 0\~1 件 |

減少得最明顯的是本地化遺漏。隨著 dialogue_id 在 L3 與翻譯鍵 1:1 繫結,`dialogue_lint.py` 攔下對映遺漏,"未翻譯的臺詞進入構建"的事故幾乎消失了。上手變短也很關鍵。對新策劃可以說"只背 L0 的 4.5 頁,你的任務就照 L2 模板填",而不是"把 70 頁 Word 全讀一遍"。

老實補一句,這個效果並非一蹴而就。第一個季度只貼了一項自動評論,其餘都是手工。介面自動化是每個季度增加一項。比起分 Layer,貼自動化花的時間更長。

---

## 5.1.11 更深的理由 —— 通往程式化生成的路

到這裡為止是表面的理由。"統一各領域之間的協作語言。"然而還有一個更本質的理由。Layer 分解是使程式化生成成為可能的前提。五層各自對應程式化生成中的一個角色(L0 錨點 → L1 規則手冊 → L2 正文 → L3 數值 → L4 關卡),而一旦混成一團,生成器就無法確定從哪裡讀、寫到哪裡去而崩潰——這一普遍命題在 §6.6 已整體討論過。這裡只看這個前提在敘事五層之上實際是如何運作的。

在一整塊 70 頁文件之上,生成演算法無法確定從哪裡讀、寫到哪裡去。敘事五層正好成了生成流水線的五個階段——L0 錨點、L1 輸入規則、L2 正文堆疊的位置、L3 模擬輸入、L4 驗證關卡。

前面的實操記錄其實已經是這五個階段的精簡版了。把 L0 支柱和 L1 基調作為上下文注入(錨點),在 L2 生成了正文,L3 行隨之產出,tone 違規的自我檢查模仿了驗證關卡。把人一次只讓做一個任務的事情,在同樣的結構上換成讓 generator 量產支線任務,就成了程式化生成。

往更遠走,就會這樣流動——玩家行為累積 → 世界 BT 節點狀態變化(Squad 上層) → NPC 數值變化(聲望·關注點·優先順序) → NPC 標籤+數值即為觸發條件 → 在任務雲中匹配的任務被觸發。任務不是預先全寫好,而是帶著標籤像"懸在空中的雲"一樣放著,玩家的行為一旦改變 NPC 數值,與觸發條件相符的任務就會落下來出現。這個進階模型會在 5.3 再詳細討論(含流程圖)。這裡要強調的一點是,所有這些流動都只在五層分解之上才能運作。

反過來,Layer 混在一起的團隊走不到程式化生成。一嘗試,就會因一致性事故而崩潰。想象一下金某既是養父又是叛徒的那起事故,通過生成器被自動量產出來的樣子就明白了。

不過這並不意味著一開始就要完美備齊五格抽屜。第一個季度只分離 L0 一行和 L1 規則手冊一本也就夠了。分離要循序漸進,介面要收窄。

最後關於時點的一點。Layer 分解本身,是從確定性 PCG(Procedural Content Generation,程式化內容生成)時代就有的分離。新出現的是 LLM 在那個分離之上,把自然語言正文、人設、敘事分支也處理了起來——上面的記錄裡 AI 配合金的基調寫出臺詞這件事,用 5 年前的規則表是做不到的。這套時點論會在 5.3 再展開。

下一章(5.2)將看到,在這五層之上,`lore_consistency_rule` 如何自動驗證世界觀→角色→任務的一致性,也就是從結構上攔下金某事故的檢查器。

---

## 動手試試 —— 第一次 Layer 分解

假設你從已經有一整塊世界觀文件的狀態開始。

**setup.** 在 NarrativeDocs 資料夾下建立五個空資料夾。從 `Layer0_Vision` 到 `Layer4_Build_QA`。把現有的一整塊文件原樣留著,從中只挑出"絕對不變的那一行",移到 `Layer0_Vision/narrative_pillar.md`。在 frontmatter 裡輸入 `status: locked`。讓這一個檔案不超過 4.5 頁。

**prompt.** 製作新內容時,按這個順序把上下文給 AI。

```
[narrative_pillar.md 全文]
[tone_manifesto.md 禁忌用語]
[相關 character_bible 檔案節選]

想法: "<一句話想法>"

不要違反這個上下文,先從 L2 任務檔案寫起。填好 related 塊
(requires/derives_from/affects),聖經裡沒有的新設定
不要加,需要的話就停下來詢問。
```

**verify.** 在輸出中要看兩點。(1) 實際開啟 `requires:` 裡寫的檔案,對照 AI 有沒有憑空造出那裡沒有的事實。(2) 在正文中搜索禁忌用語(有 `tone_lint.py` 就自動,沒有就用眼睛)。兩者只要有一項被命中就拒絕,並明確指出錯在哪裡後重新請求。上面記錄裡拒絕"亡妻"的,正是 (1)。

---

## 5.1.12 單人精簡版

如果你是沒有團隊、獨自制作的獨立開發者,五層可能看起來過頭。兩格就夠了。

放一張 `vision.md`(L0+L1 合併)、一個 `content/` 資料夾(L2),以及一張電子表格(L3)。QA 不另設一層,而是用在 content 檔案 frontmatter 裡只寫 `requires:` 一行的習慣來代替。每次寫新任務時,只把 `requires` 裡寫的檔案重新攤開對照,就能不翻遍 70 頁也攔下金某事故。核心不在層的數量,而在"把絕對不變的那一行單獨抽出來,每次都先給 AI 看"的習慣。那一行就是上下文錨點,無論是一個人還是中等規模的團隊,都從那裡開始。

---

### 本章要點

- 最抽象的敘事一旦用 Layer 解開,其他領域就會以同樣的模式跟上。
- L0 要小才不變,不變才能成為生成·驗收的上下文錨點。
- 比起分 Layer,在窄介面上貼自動化才是本質。
