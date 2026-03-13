# Handoff: 將 PUA Skill 轉換為 Claude Code Plugin

## 目標

將現有的 Claude Code skill 轉換為可透過 Plugin Marketplace 分發的 plugin，讓團隊成員能一鍵安裝並同步更新。

## 現有資源

- 已完成的 skill 檔案：`skills/pua/SKILL.md`（繁體中文，可直接使用）
- 內容：大廠 PUA 風格的激勵引擎，用於 Claude Code 反覆失敗時的壓力升級與系統化除錯方法論

## 要做的事

### 1. 建立新的 Plugin 專案

目標結構：

```
pua-plugin/
├── .claude-plugin/
│   └── plugin.json
└── skills/
    └── pua/
        └── SKILL.md
```

### 2. 建立 `plugin.json`

```json
{
  "name": "pua",
  "description": "Exhaustive problem-solving with corporate PUA pressure. Triggers on repeated failures, giving-up behavior, passive debugging, or user frustration.",
  "version": "1.0.0",
  "author": {
    "name": "<填入作者名>"
  }
}
```

### 3. 複製 SKILL.md

從 `skills/pua/SKILL.md` 複製到 plugin 的 `skills/pua/SKILL.md`。內容已是繁體中文，無需修改。

### 4. 命名注意事項

- Plugin name 設為 `pua`，skill name 也是 `pua`，安裝後指令為 `/pua:pua`
- 如果覺得 `/pua:pua` 不理想，可以：
  - 改 plugin name 為其他名稱（如 `motivator`），指令變成 `/motivator:pua`
  - 或改 skill name（資料夾名）為其他名稱

### 5. 發布到 Marketplace

兩種方式擇一：

**A. 官方 Anthropic Marketplace**
- 提交表單：https://claude.ai/settings/plugins/submit 或 https://platform.claude.com/plugins/submit

**B. 自建 Marketplace（推薦，適合團隊內部）**
- 建立 Git repo 託管 plugin
- 建立 `marketplace.json` 定義 plugin 清單
- 官方文件：https://code.claude.com/docs/en/plugin-marketplaces

### 6. 團隊安裝方式

```bash
/plugin install <marketplace-url-or-name>
```

### 7. 本地測試

開發期間可用 `--plugin-dir` 測試：

```bash
claude --plugin-dir ./pua-plugin
```

修改後執行 `/reload-plugins` 即可熱更新（不用重啟）。

## 參考文件

- [Create plugins](https://code.claude.com/docs/en/plugins)
- [Plugin Marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Plugins reference](https://code.claude.com/docs/en/plugins-reference)
- [Discover and install plugins](https://code.claude.com/docs/en/discover-plugins)
