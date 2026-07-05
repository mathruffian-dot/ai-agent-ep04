# AGENT_SETUP：外部工具連接指南（給所有 AI Agent 讀）

> 出處：三師爸 Sense Bar《AI Agent 基本功 EP04 — 連接外部工具》
> 適用對象：**任何 AI Agent**（Claude Code／Codex／AntiGravity／OpenCode 皆可）
> 使用方式：使用者對你說「讀這份檔案，幫我把 ○○ 接起來」，你讀完本檔後，依下列流程協助使用者完成連接。

---

## 你的任務

使用者（多半是老師，**不懂程式**）想讓你接上某個外部服務（雲端硬碟、筆記、資料庫、教學平台…）。你要：

1. **訪談**：問清楚要接什麼、要做什麼。
2. **判路**：用本檔的決策流程選出正確的連接方式。
3. **執行**：一步一步帶使用者完成，**每個授權動作先說明、經同意再執行**。
4. **驗收**：實測一次，把結果記錄下來。

**執行原則（必守）**：
- 半自動：先列計畫給使用者看，OK 再動手。
- **一次只接一個服務**，接好、測通、記錄，再接下一個。
- 使用者的話優先於本檔；本檔優先於你自己的猜測。

---

## 第一步：訪談（開工前必問）

1. **要接哪個服務？**（如：Google Drive、Obsidian、Firebase、Padlet…）
2. **要「讀」還是「寫」？**（只查資料＝讀；要寄信、發作業、寫入資料庫＝寫。寫的權限要更謹慎）
3. **確認你自己是哪款 Agent**（決定第三步的設定入口）。
4. **新電腦檢查**：確認基礎工具是否已裝（缺了先裝，裝前告知）：
   - `git --version`／`node --version`（多數 MCP server 需要 npx）／`python --version`
   - 該 Agent 本身是否登入完成

---

## 第二步：判路（決策流程）

> 背景觀念 30 秒：連接方式分「**通道**」（怎麼接：內建連接器 → MCP → CLI → 直接操控畫面）和「**鑰匙**」（用什麼授權：免鑰匙 → API Key/Token → OAuth）。**通道是水管，鑰匙是水管裡的水**，兩者搭配使用。2026 年起各家「內建連接器」底層幾乎都是 MCP——差別只在誰幫你接好。

依序問四個問題，**符合就停**：

1. **是 Google Workspace 個資服務嗎？**（Gmail／行事曆／Drive／Classroom）
   - 只是「讀」→ 用 Agent 的**內建連接器**（見第三步入口表），開關即用。
   - 要「寫」或要細緻權限 → 走**自建 GCP 專案＋OAuth 2.0**（工程較大，先跟使用者確認值不值得；只是偶爾讀，別走這條）。
   - ⚠️ **一組 API Key 讀不到 Google 個資**，別嘗試。
2. **Agent 的連接器目錄／MCP 商店裡有這個服務嗎？**
   - 有 → 直接用（底層是審核過的 remote MCP＋OAuth，最安全省事）。
3. **社群有現成的 MCP server 或官方 CLI 嗎？**（先搜：`<服務名> MCP server`、`<服務名> CLI`）
   - 有 MCP → 照該 Agent 的 MCP 設定方式安裝，鑰匙依 server 要求（API Key 貼設定檔，或 OAuth 登入一次）。**裝完要重啟 Agent 才生效**。
   - 有 CLI → 安裝後跑 `<cli> auth login` 類指令（登入一次、憑證存本機、之後自動帶）。
4. **都沒有？** → 最後手段：**直接操控畫面**（瀏覽器操控／Computer Use），借使用者已登入的狀態。先提醒使用者：這條最脆、最慢，畫面一改可能失效。

---

## 第三步：各 Agent 的設定入口

先辨識你自己是哪款，用對入口：

| 你是誰 | 連接器目錄 | 手動 MCP 設定 |
|--------|-----------|--------------|
| **Claude Code／Desktop** | claude.ai 或 Desktop 的 `Settings → Connectors`（500+ 個，連好會同步進 Claude Code） | `claude mcp add <名稱> -- <指令>` 或編輯 `.mcp.json` |
| **Codex／ChatGPT** | ChatGPT 的 `Settings → Apps`（原名 connectors；ChatGPT 連好 Codex 共用） | `codex mcp add <名稱> -- <指令>` 或編輯 `~/.codex/config.toml` |
| **AntiGravity** | IDE 內建 **MCP Store**（一鍵安裝，Google 服務齊全）；另有內建瀏覽器 `/browser` | MCP 設定檔（CLI／IDE 共用） |
| **OpenCode** | 無目錄 | 編輯 `opencode.json` 的 `mcp` 區塊（local／remote 兩型）或 plugins |

---

## 常見服務快查表

| 服務 | 通道 | 鑰匙 | 具體做法 |
|------|------|------|---------|
| **Obsidian** | MCP | 免鑰匙（本地） | 裝 Obsidian MCP（如 MCPVault），指到 vault 資料夾路徑即可，不用 token |
| **GitHub** | 連接器 或 CLI | OAuth | 內建連接器直接開；或裝 `gh` CLI → `gh auth login` |
| **Google Drive／Gmail／行事曆** | 內建連接器 | OAuth（底層） | 開 Agent 的連接器開關、登入 Google、按允許 |
| **Google Classroom** | 自建 OAuth | OAuth | 要發作業（寫入）得走 GCP 專案＋Classroom API；只是讀先試連接器 |
| **NotebookLM** | CLI（nlm） | 登入式 | 裝 nlm 工具 → `nlm login`。注意：此路較脆，偶爾要重新登入 |
| **Firebase** | MCP／CLI | 服務金鑰 | `firebase login`＋專案設定；金鑰**不可**進公開 repo |
| **Supabase** | MCP | API Key | 官方 MCP server＋專案金鑰貼設定檔 |
| **Padlet** | MCP | API Token | Padlet MCP＋使用者的 API token |
| **Notion／其他 SaaS** | MCP | API Key／OAuth | 搜 `<服務名> MCP server`，照 README 裝 |

---

## 安全守則（你必須替使用者把關）

1. **能用 OAuth 就別用 API Key**；能用連接器就別手貼金鑰。
2. **金鑰只放本機設定檔或 `.env`**，絕不寫進程式碼、絕不 commit 進 git（確認 `.gitignore` 有擋 `.env`、`*.key`）。
3. **每個授權動作前先告知**：要交出哪把鑰匙、權限範圍多大、怎麼撤銷。
4. **學生資料一律去識別化**：資料庫只存座號＋班級代號，不存真名。
5. **來路不明的 MCP server 不裝**：優先官方或高星數社群專案，裝前把來源網址給使用者看。
6. 教使用者一句收尾：**「不用的 token 要撤、API Key 要限制用途、OAuth scope 只開需要的。」**

---

## 第四步：驗收與記錄

1. **實測一次最小操作**：讀一筆資料（如列出 Drive 檔案、讀一則筆記），把結果秀給使用者。
2. 若接的是「寫」權限，**先在測試目標演練**（測試資料夾、測試看板），不要直接動正式資料。
3. **記錄**：在專案的 `agent.md`／`CLAUDE.md`／`handoff.md` 寫下：接了什麼服務、走哪條通道、用哪種鑰匙、設定檔位置、日期。下次（或換電腦）就不用重新摸索。
4. 提醒使用者：**MCP 裝完要重啟 Agent**；登入式憑證（如 nlm）失效時重跑 login 即可。

---

## 延伸資料

- 完整分類地圖與各路線口訣：同 repo 的 `EP04_大綱.md`、`基本功_外部工具連接方式總表.md`
- 線上簡報：https://mathruffian-dot.github.io/ai-agent-ep04/slides.html
- 影片：三師爸 Sense Bar《AI Agent 基本功》系列 https://www.youtube.com/@sensebar

> 版本：2026-07（連接器／MCP 生態變動快，若實際介面與本檔不符，以官方文件為準，並回報使用者本檔需要更新。）
