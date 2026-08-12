# Game Mass Translator User Guide
This guide is written for players and first-time translators. Complete section 2 once using manual web-based AI translation before trying CLI, Agent, glossary, or Player Package features.
## 1. Before you begin
### 1.1 How the tool works
Game Mass Translator collects game text and the required source snapshot in a `.rpytrans` project. You translate and review entries in the project, then choose whether to install the result in your own game or export a Player Package.
### 1.2 Four terms to know
- **Entry**: one source string and its translation.
- **`.rpytrans` project**: local SQLite user data containing the source snapshot, translations, marks, language direction, and install state. Back it up yourself; do not upload private projects to an Issue.
- **V/X/I**: V means confirmed for output, X means translate or review again, and I means intentionally ignored. Only V entries are written to a game or export.
- **Player Package**: a finished translation folder for other players; it does not include the game.
## 2. Complete your first translation
This section is the full beginner path: create a project, translate batches manually, review them, and install the result. The screenshots use the Traditional Chinese interface; switch languages from **Tools → Language / 語言** if needed.
### Step 1: Start and create a project
1. Extract the official ZIP and run the versioned EXE.
2. On the main window, click the large **Create Project from Game** icon in the common-actions toolbar. If you cannot find the icon, open **Tools → Create Project from Game…** instead.
3. Click **Browse…** beside **Game folder** and select the game root. Do not select a save-game subfolder.
4. Check the detected type, then click **Start**. The tool chooses a Ren'Py, Unity, Translator++ `.trans`, or MTool JSON workflow from the folder contents.
![「從遊戲建立專案」(Create Project from Game): choose a game folder and confirm the detected type](../assets/01-create-project.jpg)
If the root contains both a Translator++ `.trans` file and `ManualTransFile.json`, the tool asks which external project to import before engine detection. External projects take priority over engine detection.
### Step 2: Confirm the project and language direction
When the `.rpytrans` opens, inspect the left file tree, entry count, and source/target language. A Unity project can show evidence for more than one locale; confirm the direction before using an AI batch. An older project whose direction is not confirmed can still be browsed, edited, and exported manually, but AI preview, copy, and batch actions stay disabled.

When creating a Translator++ or MTool project, the tool conservatively scans for obvious system/program text. Only candidates with no manual mark and no real translation are initially marked **I**. Ordinary visible game text is not silently skipped; if a row is misclassified, remove its I mark. You can also use **Tools → Scan System/Program Text and Mark I…** to preview, confirm, apply, or undo the scan.
### Step 3: Read the main table
The **Source** column is the game snapshot; **Translation** is what you may write back. Select a row and edit it in the **Full Source / Full Translation** panes. Short text can also be edited by double-clicking a translation cell. Enter saves, Escape cancels, and clicking elsewhere saves a changed value.
![主表格 (Main table): review source, translation, and current V/X/I marks](../assets/02-project-review.jpg)
### Step 4: Generate a manual batch
1. Return to the main window and click the large **Web Batch Translation** icon.
2. Set **Maximum source characters**. An entry is never split; the batch follows the current tree, filter, and status range.
3. For the first batch, leave **Append prompt** and **Append glossary** enabled. The prompt describes the direction and format rules; the glossary adds matching terminology.
4. Click **Copy** and paste the complete batch into the web AI service you use (for example, Gemini).
![「網頁批次翻譯」(Web Batch Translation): copy the source batch on the left and paste the reply on the right](../assets/03-web-batch.jpg)
The output must preserve entry order, keep one source line paired with one translation line, and contain no explanation, Markdown heading, or extra blank line. Preserve `{tag}`, `[variable]`, `%s`, backslashes, and Ren'Py or RPG Maker control codes exactly.
### Step 5: Paste and analyze
1. Paste the complete AI reply into the right pane. Keeping a surrounding code block is acceptable.
2. Click **Analyze Result and Next Batch**. The tool removes an outer code block and checks row count, numbering, and control codes.
3. A successful check writes translations to the project as **unconfirmed**. A row-count or control-code mismatch writes nothing from that batch; correct the reply and try again.
4. If the AI returns an `===Glossary===` section, review it in the glossary dialog. New terms are saved only after you click **Add Selected Items**.
Continue with **Next Batch** until the current range is complete. Use **Regenerate Batch** when you need a new selection. **Undo Previous Batch** restores only the most recent translation write; it does not remove glossary terms that you already approved.
### Step 6: Review and mark V
Newly pasted or manually saved translations return to the translated-but-unconfirmed state. Check meaning, tone, control codes, variables, and line breaks. Mark a row **V** when it is safe to write to the game. Use **X** when it needs another translation and **I** when the original should intentionally remain.
![標記 V/X/I (V/X/I marks): green V is output, orange X needs another pass, and red I is ignored](../assets/04-review-marks.jpg)
Use Shift to select a range, Ctrl-click to add or remove rows, and Ctrl+A to select every row in the current filtered range. Applying V to multiple rows skips rows already marked I; select one row by itself when changing I directly to V. Before installation, filter for unconfirmed or X entries to focus the remaining review.
### Step 7: Install and verify in the game
1. Confirm that at least one row is V and save the project.
2. Return to the main window and click the large **Install Translation to Game** icon. For MTool or Translator++ projects, the same entry shows the corresponding export action and does not rewrite the source JSON or `.trans` file.
3. Choose the correct game folder and read the language direction, target files, file count, and warnings.
4. Enable only options you understand. Specialized Unity or Ren'Py routes require explicit confirmation.
5. Click **Install Translation to Game** and wait for a success summary. If **Launch game after installation** is checked, the tool attempts to start the game; otherwise launch it yourself and switch to the target language.
![「安裝到遊戲」(Install Translation to Game): confirm the target folder, language code, and installation options](../assets/05-install-to-game.jpg)
The basic success condition is a successful summary, the correct in-game language, and at least one V-marked entry visible as a translation in the game.
## 3. Main window, editing, and marks
### 3.1 The current range
The left file tree, context/source/translation filters, and status dropdown form one **current range**. The table, Ctrl+A, search and replace, and web batches all use it. Check the count and range shown in the pager before applying a bulk action.
### 3.2 Editing rules
- The Source column is a snapshot and cannot be edited directly. Recreate or re-import a project when the source itself changes.
- The full translation pane supports right-click copy, cut, and paste. Select one line and use **Add Glossary Term** to create a term.
- Embedded newlines and backslashes are data. In a batch, `\n` is a reversible representation; the tool restores it when the result is pasted back. Do not merge or split entries yourself.
- Saving a new translation clears V and X so you review it again. I remains because it represents an intentional decision not to output.
### 3.3 What V/X/I do
| Mark | Meaning | Install/export | Next batch |
|---|---|---|---|
| V | Confirmed | Written | Skipped |
| X | Translate again | Not written | Selected again |
| I | Ignore | Not written; game keeps original | Skipped |
| No mark with translation | Translated but unconfirmed | Not written | Waiting for review |
## 4. Three translation methods
| Method | Best for | How text leaves the machine | Main benefit |
|---|---|---|---|
| Manual web batch | First-time users and careful review | You copy text to a web AI | Easiest to understand and fully user-controlled |
| CLI automatic translation | Users already signed into an official CLI | The tool invokes your selected CLI | Repeats batching, writing, and retries automatically |
| Agent automatic translation | Users of Claude Code, Codex CLI, or another coding agent | The agent claims batches through a local endpoint | The agent can resume while the GUI keeps review and install authority |
All three methods share batch validation, glossary accumulation, and the rule that translations remain unconfirmed until you mark V. A project can have only one unfinished automatic job at a time.

Whichever method you use, a batch may send the selected source text, prompt settings, and matching glossary terms; it does not send the complete `.rpytrans` project or game files. The service's policies govern how the data is stored and used. See [Privacy](../PRIVACY.md).
### 4.1 CLI automatic translation (optional)
Click **CLI Automatic Translation…** in the web batch window. Refresh detection, choose an official CLI that you installed and signed into yourself (Claude Code, Codex CLI, Grok Build, or Google Antigravity), then choose the current range or whole project, per-batch entry and character limits, and retry count.
![「CLI 自動翻譯」(CLI Automatic Translation): confirm the backend, range, batch limits, and retries](../assets/06-cli-automatic.jpg)
Detection reads versions only; it does not send a translation request. The consent message lists the source text, prompt, and matching terms that will be sent, not the complete `.rpytrans` database. The project is temporarily read-only while running. A failed batch is never partially written. Sign-in, allowance, timeout, and network failures pause without pretending to skip entries. Progress is stored in `.rpytrans` and can resume; automatic translations still require manual review and V marks.
### 4.2 Agent automatic translation (optional)
On first use, click **Install Agent Skill…** in the Agent window and approve installation into the coding agent you use. Then click **Agent Automatic Translation…** in the web batch window, choose the range, limits, and retries, and click **Create and Wait for Agent**.
![「Agent 自動翻譯」(Agent Automatic Translation): create a job and wait for the external agent to claim batches](../assets/07-agent-automatic.jpg)
The tool exposes pending batches, validates submissions, and reports progress through a local loopback endpoint. The agent cannot choose a game, change the range, mark V, or install a translation. Return to the GUI and review all results when the job finishes. Stopping a job invalidates unclaimed tokens; completed and validated translations remain.
## 5. Prompts, glossary, and diagnostics
### 5.1 Edit the prompt
Click **Edit Prompt…** in the web batch window to choose the target language, inspect available variables, preview the rendered prompt, and save a project prompt. Common variables include `${source_language_name}`, `${source_language_code}`, `${target_language_name}`, `${target_language_code}`, `${target_style}`, and `${engine_format_rules}`.
![「編輯提示詞」(Edit Prompt): inspect variables, style instructions, and fixed format rules](../assets/08-edit-prompt.jpg)
**Save** changes only the current project. **Set as My Default** saves a per-language default on this computer. The fixed format section is required by the batch parser; keep the instructions about preserving control codes and one-to-one lines. Unknown variables prevent saving and batch generation.
### 5.2 Glossary and Mismatch
Open **Glossary…** from the toolbar to add, edit, delete, import, or export a UTF-8 TSV glossary. Glossary terms are embedded in `.rpytrans` and are not automatically shared between projects. Select one line in the full source or translation pane and use **Add Glossary Term** to prefill a pair.
![「術語」(Glossary): manage source terms, translations, and Mismatch results](../assets/09-glossary.jpg)
**Mismatch** finds entries whose source contains a glossary term but whose translation does not contain its required translation. It is a review warning: it does not rewrite text or block installation. Correct the translation, analyze again, and mark the reviewed row V.
### 5.3 Search, replace, and diagnostics
Use the context/source/translation filters at the top to narrow the current range. **Tools → Translation Diagnostics** checks format, untranslated coverage, and other warnings. Diagnostics are read-only; they do not change translations, marks, or game files.
## 6. Engine routing and input preparation
Use this table to choose a route. If you are unsure, select the game root and let the tool report the detected type instead of guessing individual files.
| Source | Create project from | Available route | Important boundary |
|---|---|---|---|
| Ren'Py | A folder containing `game/`, `.rpa`, or `.rpy` | Translation project and Player Package | Source or built-in baseline changes create explicit conflicts |
| Unity/XUnity.AutoTranslator | A Unity folder containing `<Game>_Data` | XUAT dictionary translation and font setup | The tool asks before acquiring missing components |
| Unity/Naninovel | A Unity IL2CPP x64 game whose text map is verified | Direct mode and Player Package | Offered only after verification; first launch may build a cache |
| Unity Mono static patch | A folder with a verified Mono target | Static patching | Advanced and offered only for recognized targets |
| Translator++ `.trans` | A `.trans` file at the game-folder root | A new `_translated.trans` file | Open the new project in Translator++ |
| MTool JSON | `ManualTransFile.json` at the root | MTool translation JSON | Useful for games with dynamic name replacement |
### 6.1 Ren'Py
The tool can read loose or RPA sources and preserves the built-in baseline. During re-import, source or identifier changes appear as conflicts; unresolved conflicts are not installed.
### 6.2 Unity/XUnity.AutoTranslator
The standard route uses an XUAT dictionary and `AutoTranslatorConfig.ini`. If BepInEx or XUnity is missing, the tool asks before downloading the required components. For missing Chinese glyphs, use the installation summary to choose the TTFLoader, MoeFont, or yozai route; some font workflows require 7-Zip.
### 6.3 Naninovel and Unity Mono
Naninovel direct mode checks bundles, catalogs, bridges, and fonts in staging. The first IL2CPP launch may take one or two minutes to build interop caches. Mono static patching is offered only when the tool recognizes a supported target.

Older Naninovel v1 projects are import-only; direct installation and Player Package export are blocked. Create a clean project from the game with a verified Naninovel v2 structure, then import the translations from the older project.
### 6.4 Translator++ and MTool
For RPG Maker, Translator++ `.trans` is usually preferred because it preserves complete `data/*.json` fields. Consider MTool when a game heavily relies on dynamic name replacement. Translator++ flow: create and save a `.trans` in Translator++ → translate here → export `_translated.trans` → open the new project in Translator++. MTool flow: create a project → translate and mark V → use the toolbar export action.
## 7. Install to your own game
Close the game before installing, back up saves and important settings, and read the installation summary. Only V entries are output; unconfirmed, X, and I entries keep the original text.
- Ren'Py writes the selected locale overlay and does not repack the original RPA.
- Standard Unity/XUAT normally writes only sidecars, configuration, and confirmed required components, not `*_Data`.
- Naninovel direct mode and Mono static patching explicitly list `*_Data` writes and require confirmation each time.
- MTool shows **Export MTool JSON** rather than writing the game. For Translator++, open the new `.trans`, then use **Export Project → Export to Folder** to write the game.
Read the success summary and backup location before launching a short test. If a game update causes a baseline or hash mismatch, do not force an overwrite; recreate the project for the new version and import only translations you can re-confirm.
## 8. Create a Player Package
A Player Package is an output for other players and does not include the game. Test the translation in your own copy first:
1. Mark every entry you intend to share as V and test it in-game.
2. For a Ren'Py `.rpa` package, install first and launch once so Ren'Py compiles the generated `.rpy` files into `.rpyc`.
3. Use **Create Ren'Py Player Package** in the advanced installation area, or choose the full or dictionary-only package for the Unity route.
4. Share the output folder together with its notices and instructions. Existing output is never overwritten; duplicate names become `(2)`, `(3)`, and so on.
Confirm that you have the right to distribute the translation and support files. Do not put the game, a private `.rpytrans`, or the tool ZIP in the package.
## 9. Troubleshooting
**Windows shows Unknown Publisher.** The public EXE is not signed. Confirm that the file came from the [official Releases](https://github.com/johnex2x/Game-Mass-Translator/releases), then follow the Windows prompt if you choose to run it.
**The game has no translation.** Confirm that entries are V, the language direction and engine route are correct, then inspect the installation summary and BepInEx/game logs.
**The AI reply has the wrong number of lines.** Regenerate the same batch and ask for one translation line per source line. Do not combine multiple batches or remove the line breaks after the entry numbers.
**The font shows squares.** Follow the Unity installation summary for the root TTF, loader/AssetBundle, and 7-Zip. You can verify the dictionary installation first and then retry another font route.
**Installation is refused after a game update.** This is usually drift or a baseline mismatch. Keep the old project and backup, create a project for the new version, and import only translations you can review again.
For other questions, use [GitHub Issues](https://github.com/johnex2x/Game-Mass-Translator/issues). Report vulnerabilities through the [private security channel](../SECURITY.md).
