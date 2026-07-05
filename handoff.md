# EP04 交接檔（handoff）

> 專案：《AI Agent 基本功》EP04 — 連接外部工具
> 最後更新：2026-07-02 ・ 更新者：Claude（覆審 Codex 修訂＋番號校正）

## ⏯️ 目前做到哪

EP04 從零規劃完成，已產出三份交付物（都在 `EP04/`）：

1. **`EP04_大綱.md`（v3，定稿）** — 完整大綱，含開場鉤子、核心地圖、兩條階梯、搭配圖說明、非 Google／Google 兩大段、操控畫面、三步選路、安全、新手起手式、口訣總表、60 分鐘節奏表、素材對照。
2. **`slides.html`（20 頁）** — 沿用 EP03 深空主題框架，鍵盤／點擊／觸控切頁，可離線。第 8 頁嵌入搭配圖 SVG，第 19 頁為 QR 下載頁。
3. **`基本功_外部工具連接方式總表.md`** — AntiGravity／Codex 基本功中用過的外部工具連接路線總表。
4. **`AGENTS.md`** — 本專案 Agent 工作邊界與外部 Padlet 模組引用註記。
5. **`channel_key_pairing.svg`** — 「通道×鑰匙」搭配接線圖（深空配色，獨立檔）。

## 🧭 本集定案（重要脈絡）

- **定位**：分類地圖集（非 demo 集），舊操作畫面引用四套基本功 lazy-packs，不重拍。
- **片長約 60 分鐘**；**雙重用途**：教學影片 ＋ 餵給 AI Agent 的第二大腦知識源 → **完整優先於精簡**。
- **主軸**：Google 家 vs 非 Google（按擁有者切）× 簡單路／完整控制路（2×2）。
- **底層兩軸**：通道（連接器/MCP/CLI/操控畫面）× 授權（免鑰匙/API Key/OAuth），比喻「水管 vs 水」；兩條階梯同向「隱性→顯性」，搭配圖首尾對調證明兩軸獨立。
- **Google 家 = 6 服務**：Gmail／行事曆／Drive／Classroom（Workspace 個資→OAuth）＋ NotebookLM（登入式）＋ Firebase（服務金鑰）。
- **Supabase 歸非 Google**（Firebase 的獨立替代品）。
- 番號以實際上架線為準（EP01→02→03→04→05 Skill），忽略舊《AI Agents 10 集進階規劃》。

## ✅ 已完成（2026-07-02 追加）

- **Git + GitHub repo**：`mathruffian-dot/ai-agent-ep04`（**public**，因 Pages 需要），branch `master`。
- **GitHub Pages**：已上線 → https://mathruffian-dot.github.io/ai-agent-ep04/slides.html （驗證 HTTP 200）。
- **素材包**：`README.md`、`qr_ep04.png`（指向 Pages 簡報），簡報加了第 19 頁 QR 下載頁（總 20 頁）。

## ✅ 已完成（2026-07-02 Codex 審核修訂）

- **修正頁數不一致**：`README.md`、`handoff.md` 已從 19 頁改為 20 頁，與 `slides.html` 實際投影片數一致。
- **修正 Google Workspace 表述**：第 13 張投影片與大綱不再寫「控制力遞增：連接器 → OAuth → 服務帳號 → API Key」，改成「Google Workspace 接法比較」，避免誤導觀眾以為 API Key 是更高控制力。保留重點：API Key 不能讀 Drive／Gmail／Classroom 個人資料。
- **補強老師場景**：README、大綱、投影片第 12 張補入 Drive 整理教材、Classroom 抓學生名單與繳交狀態、Firebase／Supabase 課堂遊戲記分、Padlet 課程牆等應用。
- **補強舊影片對照**：README 與大綱補入可回扣的實際系列標題：GPT Codex EP03、Claude EP09／EP095、AntiGravity EP06／EP07、Claude NotebookLM 系列等。
- **補強安全口訣**：大綱與第 16 張投影片加入「不用的 token 要撤、API Key 要限制用途、OAuth scope 只開需要的」。
- **補手機版排版**：`slides.html` 增加窄螢幕 CSS，手機寬度改為從上方開始排版，縮小表格、卡片與間距，避免長表格被置中裁掉。
- **補簡報導覽**：`slides.html` 加入上一頁／下一頁按鈕、PageUp／PageDown、Home／End、URL hash 記頁功能，重新整理可回到目前頁。

## ✅ 已完成（2026-07-02 路線總表補強）

- **新增 `基本功_外部工具連接方式總表.md`**：整理 AntiGravity 與 Codex 基本功中實際用過的外部工具連接路線。
- **AntiGravity 路線已收**：GitHub + Firebase、Netlify + GAS、Google Classroom、Padlet。
- **Codex 路線已收**：GitHub + Obsidian、Firebase、外掛 + Skills。
- **刻意未納入**：Google 雲端／GCP 細部設定與 Gemini Canvas，依使用者要求本次不碰。
- **README / 大綱已掛連結與對照**：README 檔案表新增總表；大綱「引用既有素材」補 AntiGravity／Codex 路線。

## ✅ 已完成（2026-07-02 Padlet 模組引用註記）

- **新增 EP04 `AGENTS.md`**：標明可引用外部 Padlet 模組：`G:\我的雲端硬碟\2026邀約\Padlet模組`。
- **新增 Padlet 模組 `AGENTS.md`**：標明模板使用順序、引用註記、Do / Don't、安全限制。
- **更新 Padlet 模組索引**：`00_Padlet模組索引.md` 增加 Agent 引用註記。
- **更新 README**：新增「Padlet 模組引用」段落，說明外部來源、用途與安全邊界。
- **引用規則**：可引用模板架構、建板規格與檢核清單；不要把 Padlet token、API key、登入資訊、學生個資放進 repo 或共用模板。

## ✅ 已完成（2026-07-02 Claude 覆審修訂）

- **番號校正（對 Obsidian vault 逐一驗證）**：
  - `EP095` → **`EP09.5`**（Claude基本功EP09.5 - Firebase串接免費資料庫），README／大綱／總表三處統一。
  - 系列名稱統一為 vault 標題格式：**「Codex基本功 EPxx」**（原混用 GPT Codex／GPTcodex／Codex 三種寫法）。
  - **GitHub + Firebase 路線代表片：EP03 → EP05**。經 AntiGravity 系列索引驗證：EP03=Netlify+GAS+GitHub（無 Firebase）；**Firebase 在 EP05**《用AI打造教學網頁的五個階段》。
  - **NotebookLM 引用修正**：原「Claude EP03／04／06」→「Claude基本功 EP03／EP04、**GoogleAI基本功 EP06**」。Claude EP06 是駕駛艙集；《Notebook LM 五大場景》其實是 GoogleAI基本功 EP06。
  - **拿掉總表對「GoogleAI EP05」的引用**：該集是 Google Canvas，與總表自己聲明的排除範圍矛盾。
- **公開／內部資訊分界**：README 移除「Padlet 模組引用」段（含本機路徑，屬內部指引，AGENTS.md 已完整涵蓋）。
- **對照表收斂為單一事實來源**：舊影片對照統一以 `基本功_外部工具連接方式總表.md` 為準；README 與大綱尾段改為指向總表，內文回扣表保留（避免三份對照彼此漂移）。
- **commit + push**：總表、AGENTS.md 與本輪修訂已進版並部署。

## ✅ 已完成（2026-07-02 連接器查證補充）

- **查證四家 Agent 的內建連接器現況**（Claude Connectors 目錄 500+／ChatGPT Apps（原 connectors）／AntiGravity MCP Store／OpenCode 無目錄純設定檔），來源：官方文件與 help center。
- **關鍵觀念入稿**：2026 年內建連接器底層幾乎全是 MCP（連接器＝原廠裝好的 remote MCP＋OAuth）；階梯 B 四階是「自己動手多少」的光譜、非互斥技術。口白：「拆開來看，走的都是同一條 MCP 標準線，差別只在誰幫你接。」
- **三處同步**：大綱階梯 B 段（升級觀念＋四家對照表）、總表（四家連接器入口對照段）、簡報第 7 頁（補一行口白註記，頁數維持 20）。

## ➡️ 下一步（未做，待決定）

- [ ] Obsidian：可在「創作庫」新增 EP04 筆記（EP01–03 都有對應筆記）。
- [ ] 錄製前可再做一次口白稿。
- [ ] 影片上架後，把實際 YouTube 連結補進 README。
- [ ] （vault 待修）Obsidian《AntiGravity基本功》索引裡 EP03 的 YouTube 連結指到 dQw4w9WgXcQ（Rick Astley），應是佔位符沒換掉。

## ⚠️ 注意事項

- `slides.html` 的 SVG 是**深空配色硬寫**（非白底），只適合這份深色簡報。
- Codex 內建連接器等產品細節在 2026-07 查證過（Codex MCP 官方文件），錄製前可再確認一次時效。
- Padlet 模組是外部共用資料夾，不屬於本 repo；引用時要註明來源路徑與實際模板檔名。
