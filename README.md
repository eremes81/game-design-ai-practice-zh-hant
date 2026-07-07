# 遊戲策劃實務即用的 AI · Claude Code 活用法

> 沒有一個數字是編造的 —— 一份歷時六個月的實戰手冊：Claude Code、提示詞、驗證與製作記憶

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](LICENSE)
[![Korean Original](https://img.shields.io/badge/原書-%ED%95%9C%EA%B5%AD%EC%96%B4%ED%8C%90%20(Korean)-blue.svg)](https://github.com/eremes81/game-design-ai-practice)
[![Print Edition (KR)](https://img.shields.io/badge/BOOKK-紙質版%20(韓語)-orange.svg)](https://bookk.co.kr/bookStore/6a298be0ff49b1a6034c7703)

**🌐 各語言版本：** [한국어 — 原書](https://github.com/eremes81/game-design-ai-practice) · [English](https://github.com/eremes81/game-design-ai-practice-en) · [日本語](https://github.com/eremes81/game-design-ai-practice-ja) · [ไทย](https://github.com/eremes81/game-design-ai-practice-th) · [Bahasa Indonesia](https://github.com/eremes81/game-design-ai-practice-id) · [簡體中文](https://github.com/eremes81/game-design-ai-practice-zh-hans) · **繁體中文**

<img src="assets/cover.svg" alt="封面" width="320">

這是一位在遊戲行業深耕 24 年的策劃總監所寫的實戰手冊，講的是如何把生成式 AI（Claude Code）真正帶進**每天的製作工作**。不是理論，也不是預測——它一次只推進一項任務，從最初的那塊螢幕（安裝、賬號、計費）開始，一路走過系統設計、戰鬥、敘事、關卡設計、數值平衡、UX，直到長期運營，再到把會議記錄變成決策、用驗證關卡守住質量、成本管理與版權。

副標題——**「沒有一個數字是編造的」**——是這本書的承諾。正文裡的每一個數字、每一個案例都來自真實的工作，而不是編造的示例；而且大部分程式碼僅憑 Python 標準庫就能原樣跑起來。

這本書也向遊戲之外的讀者敞開。把會議記錄變成決策、追溯一個決策的漣漪、用驗證關卡守住質量——這些工作流與你的職業無關都成立。每章的「遊戲之外的應用」方框就是那座橋，而每章也都帶有一節寫給獨自一人、沒有團隊者的「單人精簡版」。

---

## 🌐 關於本版本

這是韓語原書《게임 기획 실무에서 바로 쓰는 AI·클로드 코드 활용법》（BOOKK，2026 · ISBN 979-11-12-21479-9）的**繁體中文版**。

秉持本書「誠實優先」的原則，這裡如實說明本版是怎麼做出來的：它是**用本書自己的 AI 工作流從韓語原書翻譯而來**（在固定術語表約束下由 Claude 輔助翻譯），隨後由作者本人審閱——而作者並非中文母語者。所有實操記錄（worked transcript）都是對原始韓語會話的翻譯，**而非用中文重新跑一遍**；未經改動的韓語原文儲存在[韓語倉庫](https://github.com/eremes81/game-design-ai-practice)。程式碼語法、識別符號、數字與驗證值均保持原樣不動。

本繁體中文版由[簡體中文版](https://github.com/eremes81/game-design-ai-practice-zh-hans)經 OpenCC（s2twp · 臺灣用語）自動轉換派生，故遣詞用字以簡體版為準、僅作字體與臺灣慣用語轉換。**非常歡迎母語者糾錯**——若有某句讀起來不對，或臺灣在地化未盡之處，請提 Issue 或 Pull Request。

---

## 📖 從這裡開始讀

- **[序 · 如何閱讀本書](manuscript/_front-matter.md)** —— 先看這裡，瞭解各條閱讀路線
- **[1.0 開始之前 —— 安裝、賬號、計費與終端生存包](manuscript/part01-foundation/chapter-0-setup-survival-kit.md)** —— 從最初的那塊螢幕跟著走
- 圖表以 ` ```mermaid ` 程式碼塊書寫，**在 GitHub 上原生渲染**。點開下面任意一章即可閱讀。

## 韓語紙質原版

| | |
|---|---|
| 作者 | 李旼洙（이민수） |
| 出版 | BOOKK · 平裝（韓語） |
| ISBN | 979-11-12-21479-9 |
| 出版日期 | 2026-06-11 |
| 規格 | 876 頁 · 24 部分 + 附錄 A–N + 後記 |
| 購買 | **[BOOKK 商店（韓語紙質版）](https://bookk.co.kr/bookStore/6a298be0ff49b1a6034c7703)** |

本倉庫是同一本書的**繁體中文版（Markdown 源文）**，按下述許可協議釋出。韓語原書在 [eremes81/game-design-ai-practice](https://github.com/eremes81/game-design-ai-practice)。

## 完整目錄

> **24 部分 + 附錄 A–N + 後記 · 100 章。** 附錄在 [`manuscript/part99-appendix/`](manuscript/part99-appendix)，版權頁在 [`manuscript/_colophon.md`](manuscript/_colophon.md)。

### 第1部分 · 基礎

- [1.0 開始之前 —— 安裝·賬號·費用·終端生存包](manuscript/part01-foundation/chapter-0-setup-survival-kit.md)
- [1.1 遊戲策劃與 Claude Code 的第一次相遇](manuscript/part01-foundation/chapter-1-first-encounter.md)
- [1.2 模型·token·驅動框架 —— 一次任務中 token 流動的路徑](manuscript/part01-foundation/chapter-2-model-token-harness.md)
- [1.3 記憶·許可權·配置基礎設施](manuscript/part01-foundation/chapter-3-memory-permission-setting.md)

### 第2部分 · 資訊架構

- [2.1 YAML 前置後設資料 —— 讓所有文件成為資料](manuscript/part02-info-architecture/chapter-4-yaml-frontmatter.md)
- [2.2 按頁 Atom —— 單文件單決策的解剖](manuscript/part02-info-architecture/chapter-5-page-atom.md)
- [2.3 Layer 設計 —— 遊戲系統抽象化](manuscript/part02-info-architecture/chapter-6-layer-design.md)
- [2.4 本體與 wikilink 圖譜 —— 驗證語義箭頭](manuscript/part02-info-architecture/chapter-7-ontology-graph.md)

### 第3部分 · 系統設計

- [3.1 系統策劃的日常與 Layer 座標](manuscript/part03-system-design/chapter-09-system-designer-and-layer.md)
- [3.2 模式優先 —— $模式比資料更先行](manuscript/part03-system-design/chapter-10-schema-first.md)
- [3.3 關係圖視覺化 —— 用眼睛看清依賴關係](manuscript/part03-system-design/chapter-11-relation-map.md)
- [3.4 AI 輔助系統設計的提示詞模式](manuscript/part03-system-design/chapter-12-ai-assist-prompt-patterns.md)

### 第4部分 · 戰鬥設計

- [4.1 戰鬥策劃與 Layer —— 打擊感落在哪一格](manuscript/part04-combat-design/chapter-13-combat-designer-and-layer.md)
- [4.2 戰鬥 Look & Feel —— 把手感轉化為數值的環節](manuscript/part04-combat-design/chapter-14-look-and-feel.md)
- [4.3 連招·取消·輸入佇列 —— 列舉路徑並加以驗證](manuscript/part04-combat-design/chapter-15-combo-cancel-input.md)
- [4.4 AI 輔助戰鬥模擬與驗證](manuscript/part04-combat-design/chapter-16-ai-combat-simulation.md)

### 第5部分 · 敘事

- [5.1 NarrativeDocs Layer 0\~4 結構](manuscript/part05-narrative-design/chapter-1-narrative-docs-layers.md)
- [5.2 世界觀 → 角色 → 任務 的一致性驗證](manuscript/part05-narrative-design/chapter-2-consistency-verification.md)
- [5.3 AI 輔助敘事寫作](manuscript/part05-narrative-design/chapter-3-ai-assisted-narrative.md)
- [5.4 臺詞·語音一致性](manuscript/part05-narrative-design/chapter-4-dialogue-voice-consistency.md)

### 第6部分 · 內容設計

- [6.1 程式化內容生成與 AI —— 兩軸交叉的一格](manuscript/part06-content-design/chapter-1-procedural-content-ai.md)
- [6.2 city_hunting_generator —— 4 周內造出 30 座城市](manuscript/part06-content-design/chapter-2-city-hunting-generator.md)
- [6.3 NPC Persona 與 Squad —— 從玩偶博物館到小社會](manuscript/part06-content-design/chapter-3-npc-persona-squad-pipeline.md)
- [6.4 內容量產工作流 —— 把多個 generator 串成一條產線](manuscript/part06-content-design/chapter-4-content-production-workflow.md)

### 第7部分 · 關卡設計

- [7.1 程式化關卡設計總綱](manuscript/part07-level-design/chapter-1-procedural-level-design-master.md)
- [7.2 BehaviorTree 編輯器 —— 人與 AI 共同編輯並驗證 BT json 的實操記錄(worked transcript)](manuscript/part07-level-design/chapter-2-behaviortree-editor.md)
- [7.3 副本·野外模式庫](manuscript/part07-level-design/chapter-3-dungeon-field-pattern-library.md)

### 第8部分 · 數值平衡

- [8.1 戰鬥平衡公式 —— 確定性這一規則手冊的位置](manuscript/part08-balance-design/chapter-1-combat-balance-formula.md)
- [8.2 用 Machinations 建模經濟 —— 用模擬而非開會來控住通貨膨脹](manuscript/part08-balance-design/chapter-2-economy-machinations.md)
- [8.3 Damage Simulator —— 規格 DPS 與模擬結果分岔的那一天](manuscript/part08-balance-design/chapter-3-damage-simulator-2008.md)
- [8.4 AI輔助的平衡模擬](manuscript/part08-balance-design/chapter-4-ai-balance-simulation.md)
- [8.5 PvP·競技平衡 —— 勝率矩陣·匹配·伺服器權威](manuscript/part08-balance-design/chapter-5-pvp-competitive-balance.md)

### 第9部分 · UX/UI

- [9.1 把 HUD 截圖掛到 lint 上 —— 讓 AI 抓出視線偏離與對比度不足的地方](manuscript/part09-ux-ui-design/chapter-1-hud-layout.md)
- [9.2 技能按鈕排布 —— AI 生成 3 個佈局方案,lint 負責淘汰](manuscript/part09-ux-ui-design/chapter-2-skill-ui-button-column.md)
- [9.3 ArtGuide/06_UI 協作 —— 策劃用 md 寫，美術團隊只看 html](manuscript/part09-ux-ui-design/chapter-3-artguide-ui-collaboration.md)

### 第10部分 · QA

- [10.1 一致性校驗 atom —— 守護 30 張表 FK 的 cascade](manuscript/part10-qa-design/chapter-1-integrity-check-atoms.md)
- [10.2 決策驗證 3-layer 感測器 —— 人工評審證據的位置](manuscript/part10-qa-design/chapter-2-decision-validation-3-layer.md)
- [10.3 Alpha Gap Report —— 用自然語言給缺口分類,由人排定優先順序](manuscript/part10-qa-design/chapter-3-alpha-gap-report.md)

### 第11部分 · 角色·寵物·坐騎

- [11.1 命名規範與技能-美術對映](manuscript/part11-character-pet-mount/chapter-1-naming-and-skill-art-mapping.md)
- [11.2 寵物·坐騎系統 —— 從1種模板到50種例項](manuscript/part11-character-pet-mount/chapter-2-pet-mount-system.md)

### 第12部分 · 美術

- [12.1 AI 美術資產管線 —— 在可逆階段量產，在不可逆關卡前停下](manuscript/part12-art-direction/chapter-1-ai-art-asset-pipeline.md)
- [12.2 ArtGuide 七大領域(角色·動畫·怪物·NPC·VFX·UI·環境)](manuscript/part12-art-direction/chapter-2-artguide-7-areas.md)
- [12.3 規格書 → 概念 → 遊戲內資產的流轉](manuscript/part12-art-direction/chapter-3-spec-to-asset-flow.md)

### 第13部分 · 資料與 KPI

- [13.1 將數百條自由回答歸為主題——聚類交給AI,診斷交給人](manuscript/part13-data-kpi/chapter-1-faq-meta-game-analysis.md)
- [13.2 KPI 定義·追蹤 —— 定義由人來做,異常訊號診斷交給 AI](manuscript/part13-data-kpi/chapter-2-kpi-definition-tracking.md)
- [13.3 從異常指標到決策 —— AI 提出假設,人做決策](manuscript/part13-data-kpi/chapter-3-data-driven-decisions.md)

### 第14部分 · 移動端

- [14.1 PC HUD 30 種壓縮為移動端 10 種 —— 把約束變成規則手冊,把壓縮交給 AI](manuscript/part14-mobile-platform/chapter-1-mobile-hud-compression.md)
- [14.2 平臺差異(iOS / Android / PC)](manuscript/part14-mobile-platform/chapter-2-platform-differences.md)
- [14.3 觸控 / 滑鼠輸入設計](manuscript/part14-mobile-platform/chapter-3-touch-mouse-input-design.md)

### 第15部分 · 長期運營（Live Ops）

- [15.1 運營總覽 —— 活動候選由 AI 組合,規則手冊篩除,人來選定](manuscript/part15-live-ops/chapter-1-live-ops-overview.md)
- [15.2 活動·賽季運營 —— 一張模板生成 10 個變體候選,評審只由人來做](manuscript/part15-live-ops/chapter-2-event-season-ops.md)
- [15.3 把100條反饋歸為主題——聚類交給LLM,優先順序交給人](manuscript/part15-live-ops/chapter-3-user-feedback-cycle.md)

### 第16部分 · 溝通者

- [16.1 戰鬥 TF 運營 —— 在隔離的工作空間裡,只讓決策進入正本](manuscript/part16-communicator/chapter-1-taskforce-operations.md)
- [16.2 與其他工種的協作 —— 把外部請求分入三條軌道（3-track）](manuscript/part16-communicator/chapter-2-cross-job-collaboration.md)
- [16.3 一個決定,三種包裝 —— 按職能包裝產出物的 framing](manuscript/part16-communicator/chapter-3-cross-team-artifact-framing.md)

### 第17部分 · 會議記錄

- [17.1 會議記錄為何是最大的痛點](manuscript/part17-meeting-notes/chapter-1-concept-and-motivation.md)
- [17.2 從會議紀要中挖掘決策的提取管線](manuscript/part17-meeting-notes/chapter-2-extraction-pipeline.md)
- [17.3 會議分類·圖注·同步 —— 讓會議記錄成為資產的三條主軸](manuscript/part17-meeting-notes/chapter-3-categories-and-sync.md)
- [17.4 把會議記錄變成決策資料庫 —— AI 自動化的 5 個切入點](manuscript/part17-meeting-notes/chapter-4-ai-meeting-automation.md)

### 第18部分 · 決策與影響

- [18.1 決策追蹤系統](manuscript/part18-decision-impact/chapter-1-decision-tracking-system.md)
- [18.2 影響傳播·等級分類](manuscript/part18-decision-impact/chapter-2-impact-propagation-classification.md)
- [18.3 決策前後影響追蹤工作流 —— 從事前評估到事後驗證](manuscript/part18-decision-impact/chapter-3-pre-post-tracking-workflow.md)
- [18.4 文件影響面 grep 工作流 —— 用 impact 提取影響範圍](manuscript/part18-decision-impact/chapter-4-doc-impact-grep-workflow.md)

### 第19部分 · 主管與團隊領導

- [19.1 把願景用作決策的評分表 —— 將 decisions/ 中的 26 個決策交給 LLM 檢驗](manuscript/part19-team-lead/chapter-1-vision-and-delegation.md)
- [19.2 對沖突分類,不讓會議中的決策流失——會議領導力的 AI 輔助](manuscript/part19-team-lead/chapter-2-conflict-and-meeting-leadership.md)
- [19.3 AI引入戰略與說服管理層——從保守到激進,ROI 絕不加工](manuscript/part19-team-lead/chapter-3-ai-adoption-strategy.md)

### 第20部分 · 團隊協作

- [20.1 單人 DD 運營五人份的協作記憶 —— team_memory 系統](manuscript/part20-team-collab/chapter-1-team-memory-operations.md)
- [20.2 團隊成員各自的記憶 —— 使用者格與共享格的分離](manuscript/part20-team-collab/chapter-2-team-member-memory.md)
- [20.3 策劃門戶 —— 團隊通過瀏覽器進入的入口](manuscript/part20-team-collab/chapter-3-portal-web.md)
- [20.4 MCP 專案管理 —— 將協作工具與文件連線到 LLM](manuscript/part20-team-collab/chapter-4-mcp-project-management.md)

### 第21部分 · 自我改進

- [Part 21 · 第1章 覆盤是一切的起點](manuscript/part21-self-improving/chapter-1-retro-as-origin.md)
- [Part 21 · 第2章. 覆盤系統與 atom 晉升 —— 讓發現成為永久資產](manuscript/part21-self-improving/chapter-2-retro-system-atom-promotion.md)
- [Part 21 · 第3章. 閉合 self-improving 迴圈](manuscript/part21-self-improving/chapter-3-closing-the-loop.md)

### 第22部分 · 治理

- [22.1 提示詞工程 —— 遊戲策劃的一頁作業指示書](manuscript/part22-governance/chapter-1-prompt-engineering.md)
- [22.2 自信地說謊的同事 —— 用驗證關卡攔住幻覺](manuscript/part22-governance/chapter-2-ai-safety-hallucination.md)
- [22.3 AI 成本管理 —— 用程式碼守住 token 預算](manuscript/part22-governance/chapter-3-ai-cost-management.md)
- [22.4 著作權與倫理 —— 用一套流程閉合產出物的權利、標示與共識](manuscript/part22-governance/chapter-4-copyright-ethics.md)

### 第23部分 · 擴展與未來

- [Part 23 · 第1章. Wrapper·Cascade·Junction 模式](manuscript/part23-extension/chapter-1-wrapper-cascade-junction.md)
- [Part 23 · 第2章 Hermes Agent 引入實錄](manuscript/part23-extension/chapter-2-hermes-agent.md)
- [Part 23 · 第3章. 工具策展 —— 用資料裁掉不用的工具](manuscript/part23-extension/chapter-3-tool-curation.md)
- [Part 23 · 第4章. 獨自開發的益智遊戲 —— Critter Sort 實戰記](manuscript/part23-extension/chapter-4-personal-game-dev.md)

### 第24部分 · 運營實戰

- [24.1 驗證系統 —— 用程式碼揪出一致性、連結與 stale 問題](manuscript/part24-ops-deep/chapter-1-verification-system.md)
- [24.2 Mermaid 圖表自動化 —— 讓文件自己畫出自己的圖](manuscript/part24-ops-deep/chapter-2-mermaid-diagram-automation.md)
- [24.3 Wikilink 與文件層級 —— 連線與分類,檢索的兩個入口](manuscript/part24-ops-deep/chapter-3-wikilink-and-hierarchy.md)
- [24.4 來源追蹤·data lineage](manuscript/part24-ops-deep/chapter-4-source-tracking-data-lineage.md)

### 後記 · 附錄

- [後記 —— 從提問框到遊戲設計室](manuscript/part99-appendix/epilogue.md)
- [附錄 A. 公司 PC 系統詳細清單](manuscript/part99-appendix/appendix-A-company-inventory.md)
- [附錄 B. 工具借用流程(從公司到個人的通用化)](manuscript/part99-appendix/appendix-B-tool-adoption-procedure.md)
- [附錄 C. 許可權·設定參考](manuscript/part99-appendix/appendix-C-permissions-settings.md)
- [附錄 D. R&D 文件命名與 Frontmatter 標準](manuscript/part99-appendix/appendix-D-naming-frontmatter-standard.md)
- [附錄 E. MCP 伺服器目錄(遊戲策劃視角)](manuscript/part99-appendix/appendix-E-mcp-server-catalog.md)
- [附錄 F. 案例索引（公司 / 個人 PC）](manuscript/part99-appendix/appendix-F-case-index.md)
- [附錄 G. 運營指令碼案例集](manuscript/part99-appendix/appendix-G-operation-scripts.md)
- [附錄 H. 過往工作資料的複用](manuscript/part99-appendix/appendix-H-past-work-reuse.md)
- [附錄 I. BehaviorTree 編輯器案例（進階）](manuscript/part99-appendix/appendix-I-behaviortree-editor.md)
- [附錄 J. 縮略語·術語集](manuscript/part99-appendix/appendix-J-glossary.md)
- [附錄 K. 移植到其他 LLM·驅動框架(harness)](manuscript/part99-appendix/appendix-K-tool-neutral-porting.md)
- [附錄 L. 團隊匯入 TCO·上手工作表](manuscript/part99-appendix/appendix-L-team-adoption-tco.md)
- [附錄 M. 維度向量·嵌入——面向遊戲策劃的直覺](manuscript/part99-appendix/appendix-M-embedding-intuition.md)
- [附錄 N. 教學用 15 周進度表·難度指南](manuscript/part99-appendix/appendix-N-course-syllabus.md)


---

## 許可協議

本作品採用 **[CC BY-NC-SA 4.0](LICENSE)**（署名—非商業性使用—相同方式共享）許可協議。

- 允許在署名原作者（李旼洙 · 이민수）與來源的前提下進行非商業性的分享、翻譯與改編。
- 商業性使用需另行獲得作者許可。

正文中少數示例點陣圖（如 `char_skill_ui.png`）為無原圖的佔位符，可能顯示為壞圖——在正式紙質／PDF 版中這些位置已填入影像。

ⓒ 李旼洙（Minsoo Lee）2026
