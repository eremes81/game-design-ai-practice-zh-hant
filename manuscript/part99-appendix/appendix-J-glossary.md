---
title: "附錄 J. 縮略語·術語集"
appendix: J
status: v3
written: 2026-06-06
author: 이민수
version: v3
---

# 附錄 J. 縮略語·術語集

本附錄將正文中出現的縮略語與本書特有術語彙集於一處。正文會在每個縮略語首次出現處展開說明一次,但若你沒有按順序閱讀、或中途遺忘,可在此直接查詢。若同一縮略語在不同語境下含義不同,則兩種含義均予列出。

本術語集按以下順序分組:團隊規模等級 → 遊戲策劃文件 → 遊戲領域 → 資料·運營 → AI·工具 → UI·無障礙標準 → 檔案·格式。先想清楚所查縮略語的性質,便能縮小它所在分組的範圍。例如 `DPS`·`TTK` 屬於"遊戲領域",`KPI`·`DAU` 屬於"資料·運營",`atom`·`JIT` 屬於"AI·工具"分組。

標註規則有三條:① 一般縮略語同時列出正式名稱與中文釋義。② 像 `atom`·`Wrapper` 這類僅本書使用的特有術語,在正式名稱一欄標註了"(本書特有術語)"。③ 像 `PK`(戰爭語境的 Player Kill ↔ 資料語境的 Primary Key)這樣一個縮略語具有兩種含義的情況,正文在首次出現時會一併說明是哪一種,而本表中則兩種含義均予列出。

## 團隊規模等級

本書不將團隊人數固定為某個具體數字,而是用以下三個等級來表示。因為即便是同一種方法,匯入的深度也會隨團隊規模而不同。

| 等級 | 人數標準 | 說明 |
|---|---|---|
| 小規模 | \~10人 | 從單人·業餘開發者到個位數規模的團隊。通常匯入 1\~2 個階段即已足夠 |
| 中規模 | 10\~50人 | 本書運營案例所出自的作者團隊所處的區間。標準化·一致性自動化的累積效果開始變得明顯的規模 |
| 大規模 | 100+ | 多個部門·多個團隊。專用基礎設施與專職運營得以成立的規模 |

正文中像"中規模(10\~50人)團隊"這樣同時標註等級與人數範圍的地方,均以本表為準。而在像單人·獨自開發這類人數本身具有意義的場合,則不用等級,而直接寫出確切的人數。

## 遊戲策劃文件

| 縮略語 | 正式名稱 | 含義 |
|---|---|---|
| GDD | Game Design Document | 遊戲設計文件。確定了系統·數值·行為的詳細規格書 |
| CDD | Concept Design Document | 概念設計文件。GDD 之前階段的早期策劃案(方向·概念) |
| TF | TaskForce | 為短期目標而臨時組建的專職團隊(例:戰鬥 TF) |
| DD | Design Director | 設計總監。統籌遊戲設計方向的主導角色 |
| RnD | Research and Development | 研究·開發。探索原型·新技法的階段·組織(例:程式化生成 RnD) |

## 遊戲領域

| 縮略語 | 正式名稱 | 含義 |
|---|---|---|
| NPC | Non-Player Character | 玩家不操控的角色 |
| HUD | Heads-Up Display | 疊加顯示在遊戲畫面上的狀態資訊(生命值·小地圖等) |
| DPS | Damage Per Second | 每秒傷害量 |
| GCD | Global Cooldown | 全域性冷卻。使用一個技能後,所有技能都會短暫一同鎖定的公共等待時間 |
| TTK | Time To Kill | 擊殺目標所需的時間 |
| PK | Player Kill | (戰爭·PvP 語境)玩家之間的戰鬥·擊殺 |
| BT | BehaviorTree | 行為樹。將 NPC AI 的行為分支以樹形定義的結構 |
| FSM | Finite State Machine | 有限狀態機。以狀態與轉移來定義行為的模型 |
| PCG | Procedural Content Generation | 程式化內容生成。以規則·演算法自動生成內容 |
| VFX | Visual Effects | 視覺特效 |
| SFX | Sound Effects | 音效 |
| VA | Voice Actor | 配音演員 |
| RPG / MMORPG | (Massively Multiplayer Online) Role-Playing Game | 角色扮演遊戲 / 大型多人線上角色扮演遊戲 |
| P2W / P2E | Pay To Win / Play To Earn | 靠付費變強的機制 / 靠遊玩獲得收益的機制 |
| RMT | Real Money Trading | 遊戲資源的現金交易 |

## 資料·運營

| 縮略語 | 正式名稱 | 含義 |
|---|---|---|
| KPI | Key Performance Indicator | 核心績效指標 |
| DAU | Daily Active Users | 日活躍使用者數 |
| FK | Foreign Key | 外部索引鍵。指向其他表主鍵的列 |
| PK | Primary Key | (資料語境)主鍵。唯一標識一行的列 |
| ROI | Return on Investment | 投資回報(回收) |
| MECE | Mutually Exclusive, Collectively Exhaustive | 相互獨立·完全窮盡。不重複、不遺漏地進行劃分的分類原則 |
| STT | Speech-to-Text | 將語音轉換為文本 |
| VBA | Visual Basic for Applications | Excel 內建的巨集語言 |
| SVN | Subversion | 檔案版本管理系統 |
| telemetry | (計測資料) | 從遊戲構建·執行中自動收集的遊玩日誌·指標(輸入·戰鬥·流失等)。中文常稱"遙測" |

## AI·工具

| 縮略語 | 正式名稱 | 含義 |
|---|---|---|
| AI | Artificial Intelligence | 人工智慧 |
| LLM | Large Language Model | 大型語言模型(ChatGPT·Claude 等的底層基礎) |
| JIT | Just-In-Time | 僅在需要的瞬間才插入的方式(本書中指根據輸入自動注入相應記憶) |
| MCP | Model Context Protocol | 將 AI 工具與外部服務對接的標準 |
| API | Application Programming Interface | 程式間的呼叫約定 |
| UE | Unreal Engine | 虛幻引擎 |
| atom | (本書特有術語) | 以 1 決策 = 1 檔案固化而成的決策·規則卡片 |
| Wrapper / Cascade / Junction | (本書特有術語) | 常用工具的入口 / 將多項檢查一次性打包的工具 / 連線到本體的符號連結 |
| rg | ripgrep | 快速文本檢索命令(替代 grep 的 CLI 工具)。用於程式碼·文件的全量檢索 |
| ClickUp | (任務·問題追蹤器) | 管理工作·日程的雲端協作工具。JIRA·Redmine·Linear 也屬同一範疇。通過 MCP 對接,由 AI 查詢·更新 |

## UI·無障礙標準

| 縮略語 | 正式名稱 | 含義 |
|---|---|---|
| UI / UX | User Interface / User Experience | 使用者介面 / 使用者體驗 |
| WCAG | Web Content Accessibility Guidelines | Web 內容無障礙指南(對比度·觸控目標尺寸等的合格線) |
| HIG | (Apple) Human Interface Guidelines | 蘋果的介面指南 |
| SC | Success Criterion | WCAG 的單項合格標準編號(例:SC 1.4.3) |
| pt / dp / px | point / density-independent pixel / pixel | 螢幕尺寸單位 |

## 檔案·格式

| 縮略語 | 正式名稱 | 含義 |
|---|---|---|
| YAML | YAML Ain't Markup Language | 便於人閱讀的配置·資料標記格式 |
| JSON | JavaScript Object Notation | 資料交換的標記格式 |
| HTML / SVG | HyperText Markup Language / Scalable Vector Graphics | Web 文件 / 向量圖形格式 |
| GLB | GL Transmission Format (Binary) | 3D 模型二進位制檔案格式 |

---

*像 PK 這樣含義隨語境而不同的縮略語,正文在首次出現時會一併說明是哪一種。若感到混淆,回到本表檢視即可。*
