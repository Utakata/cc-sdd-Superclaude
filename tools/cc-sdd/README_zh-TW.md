# cc-sdd

**適用於 Claude Code 與 Gemini CLI：以「規格驅動開發（SDD）」變革你的開發流程**

<!-- npm badges -->
[![npm version](https://img.shields.io/npm/v/cc-sdd?logo=npm)](https://www.npmjs.com/package/cc-sdd?activeTab=readme)
[![license: MIT](https://img.shields.io/badge/license-MIT-green.svg)](tools/cc-sdd/LICENSE)

> **Beta 版本** - 可用且持續改進中。歡迎回報問題 → [Issues](https://github.com/gotalab/claude-code-spec/issues)

只需一條指令，即可安裝 **AI-DLC**（AI 驅動開發生命週期）與 **SDD**（規格驅動開發）工作流程。包含能教會 Claude Code 你的專案脈絡與開發模式的 **專案記憶（steering）**：**requirements → design → tasks → implementation**。

**相容 Kiro IDE** — 可無縫重用 Kiro 風格的 SDD 規格與工作流程。

## 🚀 快速開始

```bash
# 基本安裝（預設：Claude Code）
npx cc-sdd@latest

# 指定語言：--lang en（英）/ --lang ja（日）/ --lang zh-TW（繁中）
# 指定 OS：--os mac 或 --os windows（自動偵測失敗時使用）
npx cc-sdd@latest --lang zh-TW --os mac

# 切換為 Gemini CLI
npx cc-sdd@latest --gemini-cli

# 完成後可在助理中直接使用 `/kiro:spec-init <要打造的內容>` 開始完整 SDD 流程
```

## ✨ 你會得到什麼

- **8 個強大的 Slash Commands**（如：`/kiro:steering`, `/kiro:spec-requirements`）
- **專案記憶（steering）** — 讓 AI 學習你的程式碼庫、習慣與偏好
- **結構化 AI-DLC 流程** 與品質關卡、人工核准
- **內建 SDD 方法論**（需求 → 設計 → 任務 → 實作）
- **Kiro IDE 相容性**，流暢管理規格文件

最適用於：功能開發、程式碼審查、技術規劃、團隊開發標準維護。

## 🤖 支援的開發助理

- **✅ Claude Code** — 完整支援 8 個自訂 Slash Commands 與 CLAUDE.md
- **✅ Gemini CLI** — 完整支援 8 個自訂指令與 GEMINI.md
- **📅 更多助理** — 計畫中

（目前以 Claude Code 最佳化。使用 `--agent claude-code`（預設）以獲得完整功能。）

## 📋 AI-DLC 工作流程

**步驟 0：設定專案記憶（建議）**
```bash
# 告訴 Claude Code 你的專案脈絡
/kiro:steering
```

**SDD 開發流程：**
```bash
# 1. 建立新功能的規格
/kiro:spec-init User authentication with OAuth and 2FA

# 2. 產生詳細需求
/kiro:spec-requirements user-auth

# 3. 產生技術設計（需求審核通過後）
/kiro:spec-design user-auth -y

# 4. 拆解為任務（設計審核通過後）
/kiro:spec-tasks user-auth -y

# 5. 以 TDD 實作（任務審核通過後）
/kiro:spec-impl user-auth 1.1,1.2,1.3
```

**品質關卡**：每個階段在前進前都需要人工核准（可用 `-y` 自動核准）。

## 🎯 進階選項

```bash
# 指定語言與 OS
npx cc-sdd@latest --lang zh-TW --os mac

# 套用前預覽變更
npx cc-sdd@latest --dry-run

# 安全更新並建立備份
npx cc-sdd@latest --backup --overwrite force

# 自訂規格目錄位置
npx cc-sdd@latest --kiro-dir docs/specs
```

## 功能

✅ **AI-DLC 整合** — 完整 AI 驅動開發生命週期  
✅ **專案記憶** — Steering 會學習你的程式庫與開發模式  
✅ **規格驅動開發** — 結構化的 需求 → 設計 → 任務 → 實作  
✅ **跨平台** — 支援 macOS 與 Windows，並可自動偵測  
✅ **多語系** — 日文、英文、繁體中文  
✅ **安全更新** — 互動式提示與備份選項

---

## 📚 其他資訊

### Kiro IDE 相容性

cc-sdd 產生的規格與 steering 與 Kiro IDE 完全相容：
- 原生目錄結構：`<kiro-dir>/specs/`, `<kiro-dir>/steering/`（預設 `.kiro/`；可用 `--kiro-dir` 調整）
- 可在 Kiro IDE 中開啟/編輯，並與 Claude Code 的 Slash Commands 共用同一套文件

### 指令選項

| 選項 | 功能 | 預設 |
|------|------|------|
| `--os <auto\|mac\|windows>` | 指定作業系統（未指定時會自動偵測） | `auto` |
| `--lang <ja\|en\|zh-TW>` | 產生文件（CLAUDE.md）的語言。Commands 為英文。 | `en` |
| `--dry-run` | 僅預覽將建立/變更的檔案，不實際套用 | - |
| `--backup[=<dir>]` | 覆寫前先備份原檔 | - |
| `--overwrite <prompt\|skip\|force>` | 檔案已存在時的行為：<br>• `prompt`：逐檔確認（預設）<br>• `skip`：永不覆寫<br>• `force`：一律覆寫 | `prompt` |
| `--yes, -y` | 跳過所有提示（使 `prompt` 表現如同 `force`） | - |
| `--agent <claude-code>` | 設定要安裝指令的助理（目前僅支援 Claude Code） | `claude-code` |
| `--kiro-dir <path>` | 指定規格輸出目錄（相對於專案根目錄） | `.kiro` |

### 更多使用範例

```bash
# macOS + 繁中文件
npx cc-sdd@latest --lang zh-TW --os mac

# 安全更新（建立備份）
npx cc-sdd@latest --backup

# 跳過覆寫（保留既有檔案）
npx cc-sdd@latest --overwrite skip
```

## 輸出結構

執行 cc-sdd 後，專案將包含：

```
project/
├── .claude/
│   └── commands/
│       └── kiro/
│           ├── spec-init.md
│           ├── spec-requirements.md  
│           ├── spec-design.md
│           ├── spec-tasks.md
│           ├── spec-impl.md
│           ├── spec-status.md
│           ├── steering.md
│           └── steering-custom.md
├── .kiro/                    # 指令建立（可透過 --kiro-dir 調整）
│   ├── specs/               # 規格文件  
│   └── steering/            # AI 指導規則
├── CLAUDE.md                # 專案說明
```

## 平台支援

| 平台 | 自動偵測 | 手動指定 |
|------|----------|----------|
| macOS | ✅ `darwin` | `--os mac` |
| Windows | ✅ `win32` | `--os windows` |

## 語言支援

- **日文（`ja`）** — 日本語ドキュメント  
- **英文（`en`）** — English documentation  
- **繁體中文（`zh-TW`）** — 繁體中文文件

## 安全機制

- **互動式提示** — 覆寫前先確認
- **備份機制** — 使用 `--backup` 保留原檔
- **Dry Run 模式** — 使用 `--dry-run` 預覽所有變更
- **跳過覆寫** — 使用 `--overwrite skip` 保留既有檔案

### 檔案覆寫行為

當檔案已存在時，cc-sdd 提供三種模式：

#### Prompt（預設）
逐檔互動式確認：
```
Overwrite existing/file.md? [y]es/[n]o/[a]ll/[s]kip all:
```
- `y` — 只覆寫此檔
- `n` — 只跳過此檔  
- `a` — 覆寫後續所有檔案
- `s` — 跳過後續所有檔案

#### Skip
永不覆寫既有檔案：
```bash
npx cc-sdd --overwrite skip
```

#### Force
不提示，永遠覆寫：
```bash
npx cc-sdd --overwrite force
```

#### CI/CD 使用
在非互動環境下，預設的 Prompt 會自動退回為 Skip 並顯示警告。若要在 CI/CD 中允許覆寫，可搭配 `--yes` 或 `--overwrite force`：
```bash
# 安全的 CI/CD 更新（附備份）
npx cc-sdd --yes --backup

# 僅預覽的 CI 驗證
npx cc-sdd --dry-run
```

## 疑難排解

**在 macOS 出現 Permission denied：**
```bash
chmod +x ~/.npm/_npx/*/node_modules/.bin/cc-sdd
```

**遇到既有檔案衝突：**
```bash
npx cc-sdd --backup --overwrite force  # 安全覆寫
```

### 已知議題（Beta）
- 近期修正 Windows 模板 escaping 問題，如仍有異常請回報
- 跨平台測試仍在擴充，歡迎提供回饋
- 尚未支援自訂模板

## 回報問題與貢獻

- 問題回報：https://github.com/gotalab/claude-code-spec/issues  
- 本工具隸屬於 Claude Code Spec 專案，貢獻方式請參考主倉庫指南

## 授權

MIT License
