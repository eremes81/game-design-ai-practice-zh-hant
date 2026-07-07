---
title: "20.4 MCP 專案管理 —— 將協作工具與文件連線到 LLM"
part: 20
chapter: 4
status: v3
version: v3
written: 2026-05-24
author: 이민수
ip_check: done
---

# 20.4 MCP 專案管理 —— 將協作工具與文件連線到 LLM

週二上班後不久,9 點 12 分。我還沒開啟協作工具的看板,就先在 Claude Code 窗口裡敲下一行字。

```
顯示本週未完成的 P0 任務,按截止臨近程度排序
```

停頓了大約 3 秒,答案就出現了。我沒有直接開啟協作工具,沒有翻找儀表盤標籤頁,也沒有給負責人發即時訊息。可是一條已經逾期一天的任務被排在了最上面。我這才打開協作工具,只核對了那一張卡片。

這 3 秒是如何造出來的,就是本章的全部內容。關鍵在於,我們並沒有更換工具。專案A 團隊仍然使用協作工具(本專案用的是 ClickUp —— 一種管理任務與日程的 SaaS,JIRA、Redmine、Linear 也處在同樣的位置)。無論協作工具是什麼,本章的流程只需替換工具名稱就能照搬。資料表同樣放在 SVN 裡,決策卡也同樣放在門戶裡。改變的只有一點:LLM 現在能夠**親手開啟並檢視**這些工具了。這一連線的標準就是 MCP(Model Context Protocol)。

打個比方,這不是在前臺再多安排一名新人,而更像是把現有資料室的鎖,也為 LLM 開啟。資料室沒有變。只是多配了一把鑰匙而已。

---

## 20.4.1 MCP 究竟連線了什麼

MCP 是 LLM 訪問外部工具與資料的標準協議。"標準"二字是關鍵。它不是為協作工具單獨造一個介面卡、為文件單獨造一個、為 git 再單獨造一個,而是在 JSON-RPC 這一個約定之上,每個工具把自己暴露為"伺服器",LLM 則作為"客戶端"向該伺服器發起對話。

結構分三塊。

<svg viewBox="0 0 760 220" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="13">
  <rect x="20" y="70" width="180" height="80" rx="8" fill="#e8f0fe" stroke="#3367d6" stroke-width="1.5"/>
  <text x="110" y="100" text-anchor="middle" font-weight="bold">MCP 客戶端</text>
  <text x="110" y="122" text-anchor="middle">LLM / 使用者</text>
  <text x="110" y="140" text-anchor="middle" fill="#555">(Claude Code)</text>

  <rect x="300" y="70" width="160" height="80" rx="8" fill="#fef7e0" stroke="#f9a825" stroke-width="1.5"/>
  <text x="380" y="105" text-anchor="middle" font-weight="bold">協議</text>
  <text x="380" y="128" text-anchor="middle">JSON-RPC</text>

  <rect x="560" y="30" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="55" text-anchor="middle" font-weight="bold">MCP 伺服器 —— 協作工具</text>
  <text x="650" y="74" text-anchor="middle" fill="#555">任務檢索·查詢</text>

  <rect x="560" y="100" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="125" text-anchor="middle" font-weight="bold">MCP 伺服器 —— 文件</text>
  <text x="650" y="144" text-anchor="middle" fill="#555">決策卡·GDD 查詢</text>

  <line x1="200" y1="110" x2="300" y2="110" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="100" x2="558" y2="60" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="120" x2="558" y2="128" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <defs><marker id="a" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#666"/></marker></defs>
</svg>

伺服器會暴露一份"我能做的事"的清單。若是協作工具伺服器,就是 `search_tasks`、`get_task`、`update_task` 這樣的函式。客戶端(LLM)接收使用者的自然語言,從中挑出合適的函式來呼叫,再把返回的 JSON 用自然語言解釋出來。當我說"顯示 P0 任務"時,LLM 所做的只是呼叫了 `search_tasks(priority=P0, status=open)` 而已。

這裡要先講清楚一點。本書不講怎麼親手編寫 MCP 伺服器。像 ClickUp、JIRA、GitHub 這樣,已經有官方或社群 MCP 伺服器的工具佔絕大多數,所以策劃要做的是"安裝並連線伺服器",而不是"實現協議"。協議本身由 Anthropic 於 2024 年 11 月作為公開標準釋出,規範公開在 modelcontextprotocol.io 上。

---

## 20.4.2 實操記錄 —— "顯示本週 P0"實際要走的路

光靠嘴說"這會自動完成",聽起來像魔法。我們把實際的一次操作從頭跟到尾。下面就是這樣一段實操記錄(worked transcript,完整保留、不作刪減的真實操作過程記錄):在專案A 接入協作工具 MCP 之後,我第一次跑的會話,幾乎原樣搬來。LLM 的原始輸出不做刪減,連彆扭的地方也保留。

**① 我敲下的提示詞(全文)**

```
請在 ClickUp 中把本週截止、未完成的 P0 任務按截止臨近程度整理出來。
每一項都附上負責人和距離截止還剩的天數,已逾期的排到最上面。
```

**② Claude 的原始輸出(原樣)**

```
在 ClickUp 工作區中,按 P0·未完成·本週截止的條件做了查詢。
命中 3 條。(已把逾期的排到最上面。)

1. TASK_017  全域性冷卻程式碼變更
   負責人:teammate_a / 截止:昨天(−1 天,已逾期)
2. TASK_023  應用 voice_lint v2
   負責人:teammate_b / 截止:明天(+1 天)
3. TASK_031  更新戰鬥日誌 schema
   負責人:teammate_c / 截止:週五(+3 天)

備註:TASK_009(數值表評審)看起來也是 P0,
但它的 status 是 'in review',是否應算作"未完成"我拿不準。
沒有納入 —— 如果需要,請告訴我判定標準。
```

請注意 LLM 主動停下的這個點。`TASK_009` 處於 'in review' 狀態,它是否算"未完成",LLM 沒有擅自斷定,而是反過來問了人。MCP 能準確取回資料,但"要不要把 in review 算作未完成"取決於團隊的定義。假如 LLM 擅自做了這個判斷,那反而是事故。

**③ 我做的驗證·拒絕**

我開啟協作工具,只核對了 TASK_017 這一張卡片。確實已經逾期。但按我們團隊的標準,TASK_009 這種 'in review' 也要算進未完成。LLM 的分類和我們的規則不一樣。於是我拒絕,並重新給出了標準。

**④ 重新請求**

```
我們團隊把 'in review' 也算作未完成。請按這個標準重新整理。
今後也一律把 'in review' = 未完成來對待。
```

之後的輸出裡,TASK_009 排到了第 2 位。最後那句("今後也一律……來對待")只對本次會話生效。如果不想每次都重複同樣的規則,可以把這條定義作為 atom 錄入 `team_memory` 的 `shared` 槽位,這樣從下一次會話起 LLM 就會自動應用(參見 §20.1·§20.2)。

這一次來回說明的事很清楚。MCP 是**準確取回資訊的工具**,而**不是替人做判斷的工具**。資料是自動的,定義由人給出。一旦模糊了這條邊界,自動化就會變成事故。

---

## 20.4.3 五種應用模式

僅僅是查詢協作工具,頂多是"檢索變方便了一點"而已。MCP 成為協作系統,是在把多個工具串成一條流程的時候。下面按流程來看專案A 中實際執行的五種模式。

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="11">
  <defs><marker id="mcpar" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#888"/></marker></defs>
  <text x="400" y="20" text-anchor="middle" font-size="14" font-weight="bold">MCP 五種應用模式 —— 每種模式都是一條獨立的流程</text>
  <text x="400" y="38" text-anchor="middle" font-size="10" fill="#666">左側彩色塊是模式,右側白框是該模式所經的步驟(左→右)</text>

  <!-- 패턴 1 자동 보고서 -->
  <rect x="8" y="52" width="118" height="42" rx="6" fill="#e3f2fd" stroke="#1976d2" stroke-width="1.8"/>
  <text x="67" y="70" text-anchor="middle" font-weight="bold" fill="#1565c0">模式 1</text>
  <text x="67" y="85" text-anchor="middle" font-size="10" fill="#1565c0">自動報告</text>
  <rect x="138" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="197" y="69" text-anchor="middle" font-size="10">每天 09 點</text>
  <text x="197" y="83" text-anchor="middle" font-size="10">排程器觸發</text>
  <line x1="256" y1="73" x2="266" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="327" y="69" text-anchor="middle" font-size="10">協作工具·git·</text>
  <text x="327" y="83" text-anchor="middle" font-size="10">儀表盤查詢</text>
  <line x1="386" y1="73" x2="396" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="457" y="76" text-anchor="middle" font-size="10">LLM 合成報告</text>
  <line x1="516" y1="73" x2="526" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="528" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="587" y="76" text-anchor="middle" font-size="10">門戶/即時訊息傳送</text>

  <!-- 패턴 2 결정→태스크 -->
  <rect x="8" y="120" width="118" height="42" rx="6" fill="#e8f5e9" stroke="#388e3c" stroke-width="1.8"/>
  <text x="67" y="138" text-anchor="middle" font-weight="bold" fill="#2e7d32">模式 2</text>
  <text x="67" y="153" text-anchor="middle" font-size="10" fill="#2e7d32">決策 → 任務</text>
  <rect x="138" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="197" y="137" text-anchor="middle" font-size="10">登記決策卡</text>
  <text x="197" y="151" text-anchor="middle" font-size="9">proposal P####</text>
  <line x1="256" y1="141" x2="266" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="327" y="137" text-anchor="middle" font-size="10">在協作工具中</text>
  <text x="327" y="151" text-anchor="middle" font-size="10">建立任務</text>
  <line x1="386" y1="141" x2="396" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="457" y="137" text-anchor="middle" font-size="10">負責人·截止</text>
  <text x="457" y="151" text-anchor="middle" font-size="10">自動設定</text>

  <!-- 패턴 3 태스크→카드 -->
  <rect x="8" y="188" width="118" height="42" rx="6" fill="#fff8e1" stroke="#f9a825" stroke-width="1.8"/>
  <text x="67" y="206" text-anchor="middle" font-weight="bold" fill="#e65100">模式 3</text>
  <text x="67" y="221" text-anchor="middle" font-size="9" fill="#e65100">任務→卡片(反向)</text>
  <rect x="138" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="197" y="205" text-anchor="middle" font-size="10">協作工具</text>
  <text x="197" y="219" text-anchor="middle" font-size="10">任務完成</text>
  <line x1="256" y1="209" x2="266" y2="209" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="327" y="205" text-anchor="middle" font-size="10">決策卡</text>
  <text x="327" y="219" text-anchor="middle" font-size="9">execution_log 更新</text>

  <!-- 패턴 4 진행률 분석 -->
  <rect x="8" y="256" width="118" height="42" rx="6" fill="#f3e5f5" stroke="#7b1fa2" stroke-width="1.8"/>
  <text x="67" y="274" text-anchor="middle" font-weight="bold" fill="#6a1b9a">模式 4</text>
  <text x="67" y="289" text-anchor="middle" font-size="10" fill="#6a1b9a">進度分析</text>
  <rect x="138" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="197" y="273" text-anchor="middle" font-size="10">整個季度</text>
  <text x="197" y="287" text-anchor="middle" font-size="10">任務查詢</text>
  <line x1="256" y1="277" x2="266" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="327" y="273" text-anchor="middle" font-size="10">LLM 延期</text>
  <text x="327" y="287" text-anchor="middle" font-size="10">模式分析</text>
  <line x1="386" y1="277" x2="396" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="457" y="280" text-anchor="middle" font-size="10">季度覆盤輸入</text>

  <!-- 패턴 5 1:1 사전 자료 -->
  <rect x="8" y="324" width="118" height="42" rx="6" fill="#fff3e0" stroke="#e64a19" stroke-width="1.8"/>
  <text x="67" y="342" text-anchor="middle" font-weight="bold" fill="#d84315">模式 5</text>
  <text x="67" y="357" text-anchor="middle" font-size="10" fill="#d84315">1:1 事前資料</text>
  <rect x="138" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="197" y="348" text-anchor="middle" font-size="10">1:1 會議前 5 分鐘</text>
  <line x1="256" y1="345" x2="266" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="327" y="341" text-anchor="middle" font-size="9">成員任務 +</text>
  <text x="327" y="355" text-anchor="middle" font-size="9">team_memory·活動</text>
  <line x1="386" y1="345" x2="396" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="457" y="348" text-anchor="middle" font-size="10">自動生成事前摘要</text>
</svg>

**模式 1 —— 自動報告。** 每天早上 9 點,排程器丟擲觸發訊號,LLM 就一次性查詢協作工具的任務狀態、git 提交、儀表盤指標,寫出日報。傳送目標是門戶或團隊即時訊息工具。這裡的"門戶"指的是 §20.3 講過的公司內部門戶網頁。`server.py`(FastAPI)始終在執行,Claude 編寫的 `View_*.html` 在其上工作,所以報告也就自然地作為門戶的一個頁面疊加上去。

**模式 2 —— 決策 → 自動生成任務。** 登記決策卡(`proposal P####`)後,卡片的 implementation·verification 項就直接變成協作工具裡的任務。連負責人和截止都會自動填入。會議上"那就這麼定"所敲定的事,不經人手就落成看板上的卡片。

**模式 3 —— 任務 → 決策卡反向引用。** 是模式 2 的反方向。協作工具的任務一旦完成,MCP 就更新對應決策卡的 `execution_log`。"這個決策是否真的被執行了"會被自動追溯。決策與執行被雙向繫結(圖中的虛線)。

**模式 4 —— 進度分析。** 季度末,一次性拉取該季度的全部任務,分析延期模式。"哪一類任務反覆被拖延"成為覆盤的輸入。

**模式 5 —— 1:1 事前資料。** 1:1 會議前 5 分鐘,把該成員的協作工具任務、`team_memory` 槽位、近期活動合成為一份事前摘要。1:1 不再用"上次你在做什麼來著?"浪費 5 分鐘,而是直接從正題開始。

五種模式的共同點只有一個:**只有在減少留給人手的重複勞動的地方,價值才被回收。** 為了顯得酷炫而加上的模式,只會增加運營負擔。

---

## 20.4.4 分階段引入 —— 不要一次全接上

第一天就把五個 MCP 伺服器全部連上,是最常見的失敗。是有順序的。

| 階段 | 做什麼 | 時間感 |
|---|---|---|
| 1 | 安裝 1 個 MCP 伺服器(ClickUp 或 JIRA) | 1\~2 天 |
| 2 | 試點 1 個模式(自動報告) | 約 1 周 |
| 3 | 運營 5 個模式 | 1\~2 個月 |
| 4 | 自研 MCP 伺服器(需要特殊工具時) | 1\~3 個月 |

以上時間是以專案A 的中等規模(10\~50 人)團隊為準的作者估計,未經驗證。它會隨團隊規模、工具熟悉度而變化。可以確定的是:**大多數團隊走到 1\~3 階段就夠了**。第 4 階段(自研伺服器)只有在必須接入市面上沒有 MCP 伺服器的特殊內部工具時才走。即使不走到那一步,效果的大部分也已被回收。

單獨提一句 JIRA 是有理由的。如果說 ClickUp 是團隊內部的看板,那麼 JIRA 往往是與發行商、外包這類**外部組織共享**的工具。接上 JIRA MCP,就能在每週會議前自動拉取外包看板的進度,提前篩出疑似延期的任務。會議不再從"現狀同步"開始,而是從"決策"開始。不過,越是對外共享的工具,下一節的許可權·洩露陷阱就壓得越重。

---

## 20.4.5 四個陷阱 —— MCP 為何是雙刃劍

MCP 是把工具交到 LLM 手裡的事。手裡握的若是刀,也可能被割傷。

**陷阱 1 —— 許可權事故。** 如果 LLM 連 write 許可權也握著,就會發生意料之外的變更。一句"整理一下",就把一批任務狀態全改掉,便是這種情形。處方很明確:**MCP 伺服器從 read-only 起步。** write 只在模式 2·3 這類確有必要的地方開放,而且要在執行前設一道確認關卡再開。前面的實操記錄裡,LLM 就 'in review' 的分類反過來問人,也是同一種精神 —— 拿不準就停下。

**陷阱 2 —— 資料洩露。** 用 MCP 拉來的公司資料會被髮送到外部 LLM API。數值、未公開內容、營收指標都可能原樣流出。處方是:對敏感資料改用自託管 LLM,或在 MCP 伺服器一端替換為 placeholder 再發出(與本書通篇的 IP 保護原則一致)。

**陷阱 3 —— 依賴暴增。** 把 5 個 MCP 伺服器都掛在 critical 路徑上,只要一處掛掉,整份早間報告就停擺。處方是:只把核心的 1\~2 個設為 critical,其餘分離為輔助。輔助伺服器掛掉時,只是那一項空缺,報告本身照常產出。

**陷阱 4 —— API 成本暴增。** 一次 MCP 呼叫會同時燒掉 LLM 的 token 和外部 API 呼叫。若把自動報告每 5 分鐘跑一次,成本會悄悄膨脹。處方是:給呼叫頻率設 cap,對不常變化的查詢結果做快取。

把四個陷阱歸成一句話,MCP 的安全位置就是:**"從 read-only 起步,只把核心設為 critical,過濾敏感資料,給呼叫設上限"**。

---

## 20.4.6 效果 —— 時間從哪裡被回收

這是專案A 在運營 MCP 前後體感到的變化。下面的時間數字是作者的經驗估計(未經驗證),請不要當作絕對值,而應作為**方向與比例**來讀。

| 事項 | 無 MCP | 運營 MCP | 方向 |
|---|---|---|---|
| 日報資訊彙總 | 手動 30\~60 分鐘 | 自動 \~5 分鐘 | 大幅縮短 |
| 工具間資訊同步 | 人工手動 | 自動 | 消除手動 |
| 1:1 事前準備 | 10\~15 分鐘 | 自動摘要 \~3 分鐘 | 縮短 |
| 外包進度掌握 | 只靠會議 | 即時查詢 | 常態化 |
| 決策 ↔ 任務關聯 | 手動 | 雙向自動 | 防止遺漏 |

最大的回收來自"收集資訊的時間"。決策與判斷依然是人的工作。MCP 減少的是它前面那一段 —— 翻找散落的工具、把資訊彙集到一處的簡單勞動。本章開頭的那 3 秒,正是這個位置。

---

## 20.4.7 第 20 部分收尾

第 20 部分把團隊協作系統壘成了四層。

| 章 | 核心 |
|---|---|
| 20.1 | atom 運營 —— 類別分類、季度整理 |
| 20.2 | 團隊成員記憶 —— `team_memory` 5 人槽位(leeminsoo·團隊成員 A/b/c·shared),共享 vs 個人分離 |
| 20.3 | 門戶網頁 —— 用 `server.py`(FastAPI)·`build_index.py`·nginx·nssm 常態執行,`View_*.html` 工作 |
| 20.4 | MCP —— 5 種模式·分階段引入·許可權優先 |

這四章不是各自為政的工具,而是一個整體。門戶(20.3)是報告疊加的地方,atom 與記憶(20.1·20.2)是 LLM 記住"in review = 未完成"這類團隊定義的地方,MCP(20.4)則是把這一切與協作工具、文件連線起來的線路。任何一項被單獨拆走,其餘各項的價值也會減半。

下一部分講治理與運營。把工具接到這個程度之後隨之而來的安全性、成本、版權、倫理問題,會把本章的這些陷阱提升為團隊層面的規則來梳理。

---

### 本章要點

- MCP 是一種不更換工具、只為 LLM 配出既有工具鑰匙的標準。
- 資料由 MCP 取回,定義與判斷由人給出 —— 這條邊界就是安全線。
- 從 read-only 起步、只把核心設為 critical,自動化就不會蔓延成事故。

---

## 20.4.8 動手試試 —— 首次連線 ClickUp MCP

**setup**
1. 安裝 ClickUp MCP 伺服器(官方或社群),並申請 ClickUp API token。
2. 在 Claude Code 設定中註冊 MCP 伺服器,但只以 **read-only 作用域** 起步。
3. 確認工作區 ID,把查詢範圍限定在自己的看板。

**prompt**
```
請在 ClickUp 中把本週截止、未完成的 P0 任務按截止臨近程度整理出來。
附上負責人和距離截止還剩的天數,已逾期的排到最上面。
```

**verify**
1. 從輸出的任務中挑 1 條,在 ClickUp 中直接開啟,核對截止與負責人是否正確。
2. 看 LLM 是否就模糊的條目主動反問 —— 如果沒有反問就擅自斷定,就把分類標準寫明,再讓它重做一次。
3. 常用的定義(如 'in review=未完成')作為 atom 錄入 `team_memory` 的 `shared`,讓它在下一次會話自動應用。

### 單人精簡版

如果你是既沒有團隊、也沒有協作工具的單人開發者,MCP 的第一個物件是 **GitHub 與本地文件**。把 GitHub MCP 以 read-only 接上,從"本週未關閉的 issue,按由舊到新排序"這類查詢開始;不用決策卡,而是用文件 MCP 查詢本地 `decisions/` 資料夾裡的 Markdown。自動報告(模式 1)照樣適用 —— 只需把傳送目標從團隊即時訊息換成自己的筆記檔案即可。許可權·成本陷阱對單人也一樣存在,所以最好從一開始就守住 read-only 起步和呼叫 cap。
