# 隱私與網路說明 / Privacy and Network Notice

## 繁體中文

Game Mass Translator 沒有帳號系統、遙測、廣告或自動更新。工具不會把 `.rpytrans`、遊戲檔案、翻譯內容或診斷資料上傳給 Johnex2x。

只有在你確認特定流程後，程式才會向固定來源發出下載要求，例如：

- BepInEx、XUnity.AutoTranslator 與其必要來源檔；
- TTFLoader；
- MoeFont `yozai` 字型壓縮檔。

下載內容會以程式內釘定的 URL、版本與 SHA-256 驗證。解壓時會拒絕不安全路徑。系統 7-Zip 是你自行安裝的第三方程式，工具不會替你下載或安裝它。

### 手動網頁與 Agent 翻譯

手動網頁批次不會由工具自動上傳；你會自行決定把哪些原文複製到哪個網頁 AI。該服務如何保存與使用文字，適用該服務自己的隱私政策。Agent 自動翻譯則由你自己的 coding agent 透過本機 loopback 工作端點領取批次；本工具只驗證批次格式與寫入結果，不替你設定 agent 的模型、帳號、計費或資料保存政策。兩條路徑都可能讓遊戲原文離開本機，請在送出前確認授權與服務條款。

### CLI 自動翻譯（選用）

若你自行啟用「CLI 自動翻譯」，工具會執行**你自己安裝並登入的官方 AI CLI**（Claude Code、Codex CLI、Grok Build、OpenCode、Google Antigravity），並把該批次的內容交給它。**這代表你的遊戲原文會離開本機，送到你所選 CLI 背後的服務商。**

- 每批送出的內容只有：**所選原文、提示詞設定，以及命中的術語**。不含遊戲檔案、完整 `.rpytrans` 或其他專案內容。
- 這個功能預設關閉，必須由你選擇後端並在確認對話框同意才會啟動；對話框會逐字顯示即將執行的程式路徑。
- 工具**不儲存、不讀取、不修改、不過濾**任何 API 金鑰、OAuth token 或其他認證設定，也**不判斷、不限制、不保證**該 CLI 的計費方式。認證與計費完全由你與該 CLI 的服務商決定。
- 工具不會保留完整提示詞、遊戲文字或 CLI 對話記錄；錯誤日誌只保留截斷並去除敏感內容的診斷資訊。暫存檔在每批結束後刪除。
- 送出的資料在對方服務的保存與使用方式，適用**該服務商自己的隱私政策**，不在本工具的控制範圍內。

工具可能在你選定的遊戲資料夾留下翻譯字典、設定、`.bak`、manifest、備份與第三方授權聲明；`.rpytrans` 專案會寫在你選定的位置。安裝前的確認摘要會列出預計寫入範圍。

## English

Game Mass Translator has no account system, telemetry, advertising, or automatic updater. It does not upload `.rpytrans` files, game files, translations, or diagnostic data to Johnex2x.

Only after you confirm a specific workflow does the program download from fixed sources, such as:

- BepInEx, XUnity.AutoTranslator, and required source archives;
- TTFLoader;
- MoeFont `yozai` font archives.

Downloads are checked against pinned URLs, versions, and SHA-256 values. Unsafe archive paths are rejected. System 7-Zip is a third-party program that you install yourself; the tool does not download or install it for you.

### Manual web and Agent translation

Manual web batches are not uploaded automatically by this tool; you choose which source text to copy and which web AI service receives it. That service's own privacy policy governs retention and use. Agent automatic translation lets your coding agent claim batches through a local loopback endpoint; this tool only validates batch format and write results, and does not configure the agent's model, account, billing, or retention policy. Both paths can send game text outside your machine, so confirm your rights and the service terms before submitting text.

### CLI automatic translation (optional)

If you enable "CLI automatic translation", the tool runs an **official AI CLI that you installed and signed into yourself** (Claude Code, Codex CLI, Grok Build, OpenCode, Google Antigravity) and hands it each batch. **This means your game's source text leaves your machine and reaches the provider behind the CLI you chose.**

- Each batch carries only the **selected source text, your prompt settings, and matching glossary terms**. It never carries game files, the full `.rpytrans`, or other project content.
- The feature is off by default. You must choose a backend and accept a confirmation dialog, which shows the exact program path that will be executed.
- The tool **does not store, read, modify, or filter** any API key, OAuth token, or other credential, and **does not inspect, restrict, or guarantee** how that CLI is billed. Authentication and billing are entirely between you and that provider.
- The tool keeps no full prompts, game text, or CLI transcripts; error logs retain only truncated, de-sensitised diagnostics. Temporary files are deleted after each batch.
- How the receiving provider stores and uses that data is governed by **their own privacy policy**, which is outside this tool's control.

The tool may leave translation dictionaries, configuration, `.bak` files, manifests, backups, and third-party notices in the game directory you select; `.rpytrans` projects are written where you choose. The confirmation summary lists the intended write scope before installation.
