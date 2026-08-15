# Game Mass Translator

[繁體中文](#繁體中文) · [English](#english)

## 繁體中文

Game Mass Translator 是 Windows 桌面工具，將 Ren'Py、Unity／XUnity.AutoTranslator、Unity／Naninovel、Translator++ `.trans` 與 MTool JSON 的遊戲文字整理成可追蹤的 `.rpytrans` 專案，讓你翻譯、審核，再安裝到自己的遊戲或輸出玩家包。

目前公開版本：**1.7.0**（Windows 11 x64 驗證）。

### 下載與安全啟動

請只從 [官方 Releases](https://github.com/johnex2x/Game-Mass-Translator/releases) 下載 ZIP。下載後先在 Release 頁面核對 SHA-256 與檔案大小，再解壓縮並執行 `Game Mass Translator 1.7.0.exe`：

```powershell
Get-FileHash ".\Game-Mass-Translator-v1.7.0-win-x64.zip" -Algorithm SHA256
```

初始公開版本未簽署，Windows 可能顯示 Unknown Publisher 或 SmartScreen 警告。請核對雜湊，不要為了繞過警告而停用 Windows 安全功能。

### 五分鐘快速開始

以下流程以「手動網頁 AI 翻譯」為第一次使用的建議路線；CLI 與 Agent 自動翻譯請先完成這條流程，再參考使用手冊的進階章節。

1. 從「工具 → 從遊戲建立專案…」選取遊戲資料夾。工具會自動辨識支援的引擎或外部專案，建立 `.rpytrans` 專案。
2. 在主表格檢查原文與譯文，必要時直接編輯；尚未建立專案時不會修改遊戲來源。
3. 開啟「網頁批次翻譯」，按「複製」，把批次貼到你使用的網頁 AI（例如 Gemini），再把完整回覆貼回右側，按「分析結果並處理下一批」。
4. 逐筆複查結果。只把確定要寫入遊戲的列標記為 **V（確定）**；X 代表需要重翻，I 代表刻意忽略。
5. 按「安裝到遊戲」，確認安裝摘要中的目標資料夾、檔案數與警告，完成後啟動遊戲並切換到目標語言。

![建立專案對話框：選擇遊戲資料夾後按「開始」](assets/01-create-project.jpg)

![主表格：檢查原文、譯文與 V/X/I 標記](assets/02-project-review.jpg)

完整的逐步說明、引擎分流與疑難排解：

- [繁體中文使用手冊](docs/USER_GUIDE.zh-TW.md)
- [English User Guide](docs/USER_GUIDE.en.md)

### 支援範圍與必要條件

- 已驗證平台：64-bit Windows 11。
- Ren'Py、一般 Unity/XUnity 與 MTool／Translator++ 的基本翻譯不需要 Python 或 .NET 開發工具。
- Unity Naninovel 直接模式與 Unity Mono 靜態修補是進階流程；它們只在工具確認目標結構後才會提供。
- Unity 的字型流程可能需要系統 7-Zip。工具不會偷偷安裝 7-Zip；需要時會提供 [官方下載頁](https://www.7-zip.org/download.html)。
- 工具沒有遙測或自動更新。只有在你明確確認 Unity runtime、字型或相關安裝流程後，才會從固定官方來源下載並驗證 SHA-256。

### 資料安全與網路

抽取、編輯、預覽與診斷不會修改遊戲來源。只有你明確執行「安裝到遊戲」或輸出玩家包時，才會寫入指定目標；可修改的設定會先保留備份。

手動網頁翻譯會由你自行把文字貼到你選擇的網頁 AI。選用的 CLI／Agent 自動翻譯也可能把遊戲原文送到其背後的服務商；這些功能預設不會自動替你啟用。詳見[隱私與網路說明](PRIVACY.md)。

### 授權、支援與分享

- [軟體使用與散布條款](LICENSE.md)
- [隱私與網路說明](PRIVACY.md)
- [安全回報](SECURITY.md)
- [第三方聲明](THIRD_PARTY_NOTICES.md)

請用 [GitHub Issues](https://github.com/johnex2x/Game-Mass-Translator/issues) 回報可公開的錯誤。請移除遊戲本體、未公開內容、私人路徑與金鑰；安全漏洞請使用私人安全回報。分享翻譯成果時，只分享你有權處理的遊戲內容與 Player Package，並貼官方 Release 連結，不要重新上傳本工具 ZIP。

## English

Game Mass Translator is a Windows desktop tool that turns text from Ren'Py, Unity/XUnity.AutoTranslator, Unity/Naninovel, Translator++ `.trans`, and MTool JSON projects into a traceable `.rpytrans` project. You can translate, review, install to your own game, or export a player package.

Current public version: **1.7.0**, validated on Windows 11 x64.

### Download and safe startup

Download the ZIP only from the [official Releases](https://github.com/johnex2x/Game-Mass-Translator/releases). Compare the SHA-256 and file size shown on the Release page before extracting and running `Game Mass Translator 1.7.0.exe`:

```powershell
Get-FileHash ".\Game-Mass-Translator-v1.7.0-win-x64.zip" -Algorithm SHA256
```

The initial public build is unsigned, so Windows may show Unknown Publisher or a SmartScreen warning. Verify the hash; do not disable Windows security features to bypass the warning.

### Five-minute quick start

The recommended first route is manual web-based AI translation. Finish this route once before trying the optional CLI or Agent automation.

1. Choose **Tools → Create Project from Game…** and select the game folder. The tool detects a supported engine or external project and creates a `.rpytrans` project.
2. Review the source and translation columns in the main table and edit entries when needed. Project creation and editing do not modify the game source.
3. Open **Web Batch Translation**, click **Copy**, paste the batch into the web AI service you use (for example, Gemini), then paste the complete reply into the right pane and click **Analyze Result and Next Batch**.
4. Review the result entry by entry. Mark only entries you want written to the game as **V (Confirmed)**; X means translate again and I means intentionally ignore.
5. Click **Install Translation to Game**, verify the destination, file count, and warnings in the summary, then launch the game and switch to the target language.

![Create Project dialog: choose a game folder and click Start](assets/01-create-project.jpg)

![Main table: review source, translations, and V/X/I marks](assets/02-project-review.jpg)

For the complete step-by-step guide, engine routing, and troubleshooting, read:

- [繁體中文使用手冊](docs/USER_GUIDE.zh-TW.md)
- [English User Guide](docs/USER_GUIDE.en.md)

### Supported scope and requirements

- Validated platform: 64-bit Windows 11.
- Basic Ren'Py, standard Unity/XUnity, MTool, and Translator++ translation does not require Python or .NET development tools.
- Unity Naninovel direct mode and Unity Mono static patching are advanced paths offered only after the tool verifies the target structure.
- Unity font workflows may require system 7-Zip. The tool does not silently install it; when needed it links to the [official download page](https://www.7-zip.org/download.html).
- There is no telemetry or automatic updater. Downloads happen only after you explicitly confirm a Unity runtime, font, or related installation flow, and are SHA-256 verified from fixed official sources.

### Data safety and network behavior

Extraction, editing, preview, and diagnostics do not modify game sources. Files are written only when you explicitly install to a game or export a player package; writable configuration is backed up first.

Manual web translation means that you choose what to paste into your web AI service. Optional CLI and Agent automation can also send game source text to the provider behind the selected service, and are not enabled automatically. See the [Privacy and Network Notice](PRIVACY.md).

### Terms, support, and sharing

- [Software Use and Distribution Terms](LICENSE.md)
- [Privacy and Network Notice](PRIVACY.md)
- [Security Reporting](SECURITY.md)
- [Third-Party Notices](THIRD_PARTY_NOTICES.md)

Use [GitHub Issues](https://github.com/johnex2x/Game-Mass-Translator/issues) for public bugs after removing game files, unreleased content, private paths, and secrets. Use the private security channel for vulnerabilities. Share only game content and Player Packages you are entitled to share, and link to the official Release instead of re-uploading this ZIP.
