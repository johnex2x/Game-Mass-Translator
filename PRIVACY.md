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

- 每批送出的內容只有：**所選原文（另附每批頭尾各 3 句同一檔案的相鄰原文，僅供參考）、提示詞設定，以及命中的術語**。不含遊戲檔案、完整 `.rpytrans` 或其他專案內容。
- 這個功能預設關閉，必須由你選擇後端並在確認對話框同意才會啟動；對話框會逐字顯示即將執行的程式路徑。
- 使用 CLI 後端時，工具**不儲存、不讀取、不修改、不過濾**該 CLI 的 API 金鑰、OAuth token 或其他認證設定，也**不判斷、不限制、不保證**該 CLI 的計費方式。認證與計費完全由你與該 CLI 的服務商決定。
- 工具不會保留完整提示詞、遊戲文字或 CLI 對話記錄；錯誤日誌只保留截斷並去除敏感內容的診斷資訊。暫存檔在每批結束後刪除。
- 送出的資料在對方服務的保存與使用方式，適用**該服務商自己的隱私政策**，不在本工具的控制範圍內。

### OpenAI 相容 API 自動翻譯（選用）

若你在「API 端點設定」設定一個端點（內建的 DeepSeek，或你自己輸入位址的 OpenAI 相容服務），並在確認對話框同意，工具會把每一批內容直接送到**你設定的位址**。**這代表你的遊戲原文會離開本機，送到該服務商。**

- 每批送出的內容與 CLI 自動翻譯相同：**所選原文（另附每批頭尾各 3 句同一檔案的相鄰原文，僅供參考）、提示詞設定，以及命中的術語**，另加你選的模型名稱與推理強度。不含遊戲檔案、完整 `.rpytrans` 或其他專案內容。
- 確認對話框會逐字顯示即將連線的網址與主機。只接受 https；http 只限本機（127.0.0.1、::1、localhost）。工具不跟隨重新導向。連到非本機位址時，請求會經過 Windows 系統或環境變數設定的 proxy（若你有設定）；本機位址一律不經過 proxy。
- 偵測 API 端點不會連線。「取得模型清單」會帶著金鑰向該位址查詢模型清單；「測試連線」會再送出一個極小的請求（會花費少量 token）。兩者都不含遊戲文字。
- **API 金鑰由你輸入，工具會儲存它**：以 Windows DPAPI 用你目前的 Windows 帳戶加密，存放在 `%APPDATA%\GameMassTranslator\api_keys.json`（與 `settings.json` 同一資料夾，但不在 `settings.json` 裡）。金鑰綁定你儲存時的端點來源（協定、主機與連接埠）；來源改變後，工具不會送出舊金鑰，要求你重新輸入。金鑰只放在送往該位址的請求標頭中，不會寫入 `.rpytrans`、匯出檔、錯誤訊息或日誌。另一個 Windows 帳戶無法解密它，換到其他電腦通常也要重新輸入。你可以隨時在「API 端點設定」按「清除金鑰」刪除它；刪除端點並按「儲存設定」也會一併刪除它的金鑰。
- 端點的非機密設定（名稱、位址、模型、價格、花費上限等）存在 `settings.json`。分享該檔案時，也會一併分享你的端點位址。
- 工具會在 `.rpytrans` 裡記錄每個工作的 token 用量與你設定的花費上限，用來顯示估計費用，並在達到上限時暫停。工作記錄只存端點代號，不存金鑰或 Base URL；但暫停原因可能含主機名稱與服務回傳的簡短錯誤說明，分享 `.rpytrans` 前請留意。
- **費用估計與花費上限都有限制**：開始前顯示的用量與費用是估計值，不含重試與思考 token，實際以服務商帳單為準。上限在每一批送出前檢查，所以最後一批可能讓總額超過上限，確認對話框會顯示單批最多可能超出多少。你中止的批次可能仍會被服務商計費；工具無法得知實際用量，只會把估計值計入該工作的花費。
- 工具不查詢你的帳戶餘額，也不保證計費方式；費用由你的 API 帳戶支付，計費完全由你與該服務商決定。
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
- With a CLI backend, the tool **does not store, read, modify, or filter** that CLI's API key, OAuth token, or other credential, and **does not inspect, restrict, or guarantee** how that CLI is billed. Authentication and billing are entirely between you and that provider.
- The tool keeps no full prompts, game text, or CLI transcripts; error logs retain only truncated, de-sensitised diagnostics. Temporary files are deleted after each batch.
- How the receiving provider stores and uses that data is governed by **their own privacy policy**, which is outside this tool's control.

### OpenAI-compatible API automatic translation (optional)

If you set up an endpoint in "API endpoints" (the built-in DeepSeek preset, or an OpenAI-compatible service whose address you enter) and accept the confirmation dialog, the tool sends each batch directly to **the address you configured**. **This means your game's source text leaves your machine and reaches that provider.**

- Each batch carries the same content as CLI automatic translation: **the selected source text (plus up to 3 neighbouring lines from the same file before and after each batch, for reference only), your prompt settings, and matching glossary terms**, plus the model name and reasoning effort you chose. It never carries game files, the full `.rpytrans`, or other project content.
- The confirmation dialog shows the exact URL and host it will connect to. Only https is accepted; http is allowed only for this PC (127.0.0.1, ::1, localhost). The tool does not follow redirects. Requests to an address that is not on this PC go through the proxy set in Windows or in environment variables, if you have set one; addresses on this PC never use a proxy.
- Detecting API endpoints does not connect to anything. "Fetch model list" asks that address for its model list and sends your key. "Test connection" also sends one tiny request, which spends a few tokens. Neither sends game text.
- **You enter the API key and the tool stores it**: encrypted with Windows DPAPI under your current Windows account, in `%APPDATA%\GameMassTranslator\api_keys.json` (the same folder as `settings.json`, but not inside `settings.json`). The key is bound to the endpoint origin (scheme, host, and port) it was saved for. If the origin changes, the tool does not send the old key and asks you to enter it again. The key is placed only in the request header sent to that address. It is never written to `.rpytrans` files, exports, error messages, or logs. Another Windows account cannot decrypt it, and on another PC you will usually need to enter it again. You can delete it at any time with "Clear key" in "API endpoints"; deleting an endpoint and clicking "Save settings" also deletes its key.
- The endpoint's non-secret settings (name, address, model, prices, spend cap, and so on) are stored in `settings.json`. If you share that file, you also share your endpoint address.
- The tool records each job's token usage and your spend cap in the `.rpytrans`, to show estimated cost and to pause at the cap. The job record stores only the endpoint's code name, never the key or the Base URL; a pause reason may still contain the host name and a short error message from the provider, so check before you share a `.rpytrans`.
- **The estimate and the cap have limits**: the usage and cost shown before a job starts are estimates, exclude retries and thinking tokens, and the provider's bill is authoritative. The cap is checked before each batch is sent, so the last batch can push the total past the cap; the confirmation dialog shows the most one batch can add. A batch that you stop may still be billed by the provider; the tool cannot know the real usage, so it adds an estimate to that job's spend.
- The tool does not query your account balance and does not guarantee how you are billed; costs are paid by your API account, and billing is entirely between you and that provider.
- How the provider stores and uses that data is governed by **their own privacy policy**, which is outside this tool's control.

The tool may leave translation dictionaries, configuration, `.bak` files, manifests, backups, and third-party notices in the game directory you select; `.rpytrans` projects are written where you choose. The confirmation summary lists the intended write scope before installation.
