# AGENT_SETUP：外部工具連接指南（給所有 AI Agent 讀）

> 出處：三師爸 Sense Bar《AI Agent 基本功 EP04 — 連接外部工具》（影片：https://youtu.be/-kIzGOf0bZA）
> 適用對象：**任何 AI Agent**，特別針對四款桌面版應用校準：**Claude Code／ChatGPT App（含 Codex）／Antigravity 2／OpenCode**。
> 使用方式：使用者對你說「讀這份檔案，幫我把 ○○ 接起來」，你讀完本檔後，依下列流程協助使用者完成連接。
> 給人類讀者：全新電腦也適用——直接把這個 raw 網址丟給你的 Agent 即可：
> `https://raw.githubusercontent.com/mathruffian-dot/ai-agent-ep04/master/AGENT_SETUP_外部工具連接指南.md`

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
- 本檔寫的介面入口若與實際畫面不符（產品改版很快），以官方文件為準，並回報使用者本檔需要更新。

---

## 第一步：訪談（開工前必問）

1. **要接哪個服務？**（如：Google Drive、Obsidian、Firebase、Padlet…）
2. **要「讀」還是「寫」？**（只查資料＝讀；要寄信、發作業、寫入資料庫＝寫。寫的權限要更謹慎）
3. **確認你自己是哪款 Agent、使用者是哪個作業系統**：Agent 決定設定入口（見第三步）；作業系統決定指令寫法——**Windows 有 `cmd /c` 與路徑反斜線兩個經典坑**（見〈常見卡關排除〉）。
4. **新電腦檢查**：確認基礎工具是否已裝（缺了先裝，裝前告知）：
   - `node --version`（多數本地 MCP server 靠 npx 啟動，**沒裝 Node.js 是新手最常見的死因**）
   - `git --version`／`python --version`（視服務需要）
   - 該 Agent 本身是否登入完成

---

## 第二步：判路（決策流程）

> 背景觀念 30 秒：連接方式分「**通道**」（怎麼接：內建連接器 → MCP → CLI → 直接操控畫面）和「**鑰匙**」（用什麼授權：免鑰匙 → API Key/Token → OAuth）。**通道是水管，鑰匙是水管裡的水**，兩者搭配使用。2026 年起各家「內建連接器」底層幾乎都是 MCP——差別只在誰幫你接好。

依序問四個問題，**符合就停**：

1. **是 Google Workspace 個資服務嗎？**（Gmail／行事曆／Drive／Classroom）
   - 只是「讀」→ 用 Agent 的**內建連接器**（見第三步入口表），開關即用。
   - 要「寫」或要細緻權限 → 走**自建 GCP 專案＋OAuth 2.0**（工程較大，先跟使用者確認值不值得；只是偶爾讀，別走這條）。
   - ⚠️ **一組 API Key 讀不到 Google 個資**，別嘗試。
2. **Agent 的連接器目錄裡有這個服務嗎？**（Claude 叫 Connectors、ChatGPT 叫 Apps／Plugins、Antigravity 2 叫 MCP Store；OpenCode 沒有目錄）
   - 有 → 直接用（底層是審核過的 remote MCP＋OAuth，最安全省事）。
3. **社群有現成的 MCP server 或官方 CLI 嗎？**（先搜：`<服務名> MCP server`、`<服務名> CLI`）
   - 有 MCP → 照該 Agent 的 MCP 設定方式安裝（見第三步具體指令），鑰匙依 server 要求（API Key 貼設定檔，或 OAuth 登入一次）。**裝完要重啟 Agent 才生效**。
   - 有 CLI → 安裝後跑 `<cli> auth login` 類指令（登入一次、憑證存本機、之後自動帶）。
4. **都沒有？** → 最後手段：**直接操控畫面**（瀏覽器操控／Computer Use），借使用者已登入的狀態。先提醒使用者：這條最脆、最慢，畫面一改可能失效。

---

## 第三步：各 Agent 的設定入口

先辨識你自己是哪款，用對入口。**共通鐵律：手動裝完 MCP 要完全重啟 Agent 才生效。**

### 總覽表（2026-07-11 查證）

| 你是誰 | 連接器目錄（簡單路） | 手動 MCP 設定檔 | 驗證方式 |
|--------|---------------------|----------------|---------|
| **Claude Code**（CLI／桌面版） | claude.ai 的 `Settings → Connectors`（500+，同帳號自動同步進 Claude Code） | `claude mcp add`；專案 `.mcp.json`、使用者 `~/.claude.json` | `claude mcp list`；會話內 `/mcp` |
| **ChatGPT App（含 Codex）** | `Settings → Apps`（**2026-07 起目錄併入 Plugins**，兩個名字都找找看） | Codex：`codex mcp add` 或 `~/.codex/config.toml`；ChatGPT 自訂 MCP 要開 Developer mode | `codex mcp list` |
| **Antigravity 2** | IDE 內 **MCP Store**（`Settings → Customizations`，Google 服務最全）；另有內建瀏覽器 `/browser` | `~/.gemini/config/mcp_config.json`（**IDE／CLI 共用同一份**） | Customizations 頁看已裝清單 |
| **OpenCode** | 無目錄（最 DIY） | 專案 `opencode.json` 或全域 `~/.config/opencode/opencode.json` 的 `mcp` 區塊 | 重啟後問 Agent 有哪些工具 |

> 通用驗證招（四款都適用）：重啟後直接問 Agent「**你現在看得到哪些 MCP 工具？**」

### Claude Code：具體指令

```bash
# macOS / Linux（本地 stdio server）
claude mcp add <名稱> -- npx -y <MCP套件名>

# Windows 必須包一層 cmd /c（不包會顯示已安裝但永遠連不上）
claude mcp add <名稱> -- cmd /c npx -y <MCP套件名>

# 遠端（HTTP）server
claude mcp add --transport http <名稱> <server網址>
```

- 預設只裝在**目前專案**；想每個資料夾都能用，加 `--scope user`。
- 遠端 server 要 OAuth 登入時，在會話內打 `/mcp` 完成授權。
- claude.ai 網頁上連好的連接器（Google Drive／Gmail／行事曆…），同帳號的 Claude Code 會自動看到，不用重設。

### ChatGPT App（含 Codex）：具體做法

- **官方 apps（最簡單）**：ChatGPT `Settings → Apps`。注意：**2026-07-09 起 Apps 目錄改版併入 Plugins**——設定裡找不到 Apps 就找 Plugins。官方 apps 各方案皆可用。
- **自訂 MCP**：需先開 **Developer mode**——`Settings → Security and login` 裡開啟（**目前僅網頁版 chatgpt.com 能開**，桌面 App 裡找不到這個開關是正常的；需付費方案）。開啟後到 `Settings → Plugins`（或 chatgpt.com/plugins）按「＋」貼遠端 MCP server 網址。
- **Codex（命令列／ChatGPT 內的工程 Agent）**：

```bash
codex mcp add <名稱> -- npx -y <MCP套件名>
```

或編輯 `~/.codex/config.toml`：

```toml
[mcp_servers.<名稱>]
command = "npx"
args = ["-y", "<MCP套件名>"]
```

### Antigravity 2：具體做法

- **MCP Store（優先）**：`Settings → Customizations` → MCP Store，搜尋服務名、按 Install、照表單填資訊即可（Google 服務最齊全）。
- **手動**：同頁「Open MCP Config」會開 `~/.gemini/config/mcp_config.json`——**IDE、CLI 共用同一份，改一次全家生效**：

```json
{
  "mcpServers": {
    "本地例子": { "command": "npx", "args": ["-y", "<MCP套件名>"] },
    "遠端例子": { "serverUrl": "https://<server網址>", "headers": { "Authorization": "Bearer <token>" } }
  }
}
```

- 注意：遠端要用 `serverUrl`（不是舊版的 `httpUrl`）；JSON 檔**不能寫註解**；有使用者回報全域設定的環境變數帶不進去——金鑰若只能直接寫進設定檔，務必確認該檔不會被 commit 或分享出去。

### OpenCode：具體做法

編輯專案 `opencode.json`（或全域 `~/.config/opencode/opencode.json`）：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "本地例子": { "type": "local", "command": ["npx", "-y", "<MCP套件名>"], "enabled": true },
    "遠端例子": { "type": "remote", "url": "https://<server網址>", "enabled": true }
  }
}
```

- OpenCode 沒有連接器目錄，一切手寫——但格式就上面這兩型（local／remote）。
- 每多裝一個 MCP，它的工具說明都會吃掉一部分上下文——**只裝這個專案用得到的**。

---

## 常見服務快查表（依老師常用程度排序）

| 服務 | 通道 | 鑰匙 | 具體做法 |
|------|------|------|---------|
| **Google Drive／Gmail／行事曆** | 內建連接器 | OAuth（底層） | 開 Agent 的連接器開關、登入 Google、按允許。**別想用 API Key 讀個資，讀不到** |
| **Obsidian** | MCP | 免鑰匙（本地） | 裝 Obsidian MCP（如 MCPVault），指到 vault 資料夾路徑即可，不用 token。Windows 路徑在設定檔裡要寫 `C:/...` 或 `C:\\...` |
| **NotebookLM** | CLI（nlm） | 登入式 | 裝 nlm 工具 → `nlm login`。此路較脆，登入失效就重跑一次 login |
| **GitHub** | 連接器 或 CLI | OAuth | 內建連接器直接開；或裝 `gh` CLI → `gh auth login` |
| **Padlet** | MCP | API Token | Padlet MCP＋使用者的 API token |
| **Google Classroom** | 自建 OAuth | OAuth | 要發作業（寫入）得走 GCP 專案＋Classroom API；只是讀先試連接器 |
| **Firebase** | CLI／MCP | 服務金鑰 | `firebase login`＋專案設定；金鑰**不可**進公開 repo |
| **Supabase** | MCP | API Key | 官方 MCP server＋專案金鑰貼設定檔 |
| **Notion／其他 SaaS** | MCP | API Key／OAuth | 搜 `<服務名> MCP server`，優先官方或高星數專案，照 README 裝 |

---

## 常見卡關排除（先查這張表再求救）

| 症狀 | 最可能原因 | 解法 |
|------|-----------|------|
| 裝了 MCP 但 Agent 看不到工具 | 沒重啟 | 完全關掉 Agent 重開，再問它「你有哪些 MCP 工具」 |
| Claude Code：`claude mcp list` 顯示 failed（Windows） | npx 沒包 `cmd /c` | 移除後重加：`claude mcp add <名稱> -- cmd /c npx -y <套件名>` |
| 出現 npx／npm 找不到之類錯誤 | 沒裝 Node.js | 裝 Node.js LTS，裝完**重開終端機**再試 |
| 改了設定檔完全沒反應 | JSON 格式錯 | JSON 不能有註解與多餘逗號；Windows 路徑用 `/` 或 `\\`，單一 `\` 會壞 |
| ChatGPT 設定裡找不到「Apps」 | 2026-07 目錄改版 | 改找 **Plugins**；要接自訂 MCP 先到**網頁版**開 Developer mode |
| 遠端 MCP 一直 401／未授權 | OAuth 沒完成或過期 | Claude Code 在會話內打 `/mcp` 重新授權；其他 Agent 依提示重新登入 |
| nlm 等登入式 CLI 突然失效 | 憑證過期 | 重跑 `nlm login`（這類通道本來就偶爾要重登，不是壞掉） |
| Agent 接上一堆工具後變笨、答非所問 | MCP 裝太多吃爆上下文 | 停用用不到的 MCP，只留本專案需要的 |

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

- 本集影片：《AI Agent 基本功 EP04：連接外部工具》 https://youtu.be/-kIzGOf0bZA
- 完整分類地圖與各路線口訣：同 repo 的 `EP04_大綱.md`、`基本功_外部工具連接方式總表.md`
- 線上簡報：https://mathruffian-dot.github.io/ai-agent-ep04/slides.html
- 系列頻道：三師爸 Sense Bar https://www.youtube.com/@sensebar

> 版本：v2（2026-07-11 依四款桌面版 Agent 現況全面查證更新：ChatGPT Apps 目錄併入 Plugins、Antigravity 2 共用設定檔路徑、Claude Code Windows `cmd /c` 坑、OpenCode 設定範例、常見卡關排除表。連接器／MCP 生態變動快，若實際介面與本檔不符，以官方文件為準，並回報使用者本檔需要更新。）
