# EP04 交接檔（handoff）

> 專案：《AI Agent 基本功》EP04 — 連接外部工具
> 最後更新：2026-07-02 ・ 更新者：Claude（規劃 session）

## ⏯️ 目前做到哪

EP04 從零規劃完成，已產出三份交付物（都在 `EP04/`）：

1. **`EP04_大綱.md`（v3，定稿）** — 完整大綱，含開場鉤子、核心地圖、兩條階梯、搭配圖說明、非 Google／Google 兩大段、操控畫面、三步選路、安全、新手起手式、口訣總表、60 分鐘節奏表、素材對照。
2. **`slides.html`（19 頁）** — 沿用 EP03 深空主題框架，鍵盤／點擊／觸控切頁，可離線。第 8 頁嵌入搭配圖 SVG。
3. **`channel_key_pairing.svg`** — 「通道×鑰匙」搭配接線圖（深空配色，獨立檔）。

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

## ➡️ 下一步（未做，待決定）

- [ ] Obsidian：可在「創作庫」新增 EP04 筆記（EP01–03 都有對應筆記）。
- [ ] 錄製前可再做一次口白稿。
- [ ] 影片上架後，把實際 YouTube 連結補進 README。

## ⚠️ 注意事項

- `slides.html` 的 SVG 是**深空配色硬寫**（非白底），只適合這份深色簡報。
- Codex 內建連接器等產品細節在 2026-07 查證過（Codex MCP 官方文件），錄製前可再確認一次時效。
