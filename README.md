# C2 PUA 高效激勵引擎

> 用企業 PUA 壓力驅動 AI 窮盡一切解決問題。支援 Claude Code / Codex / Cursor。

[![版本](https://img.shields.io/badge/version-1.7.0-blue.svg)](https://github.com/hulion/nextpua)

## 這是什麼

當 AI 反覆失敗、想放棄、被動 debug 或品質低落時，PUA 引擎自動介入，用分級壓力話術 + 系統化方法論逼 AI 窮盡所有可能方案。

**不是給人用的 PUA，是給 AI 用的。**

## 安裝

### Claude Code（插件）

```bash
# 1. 新增 marketplace
claude plugins marketplace add hulion/nextpua

# 2. 安裝插件
claude plugins install c2l@nextpua
```

啟動方式：在 Claude Code 中輸入 `/c2l:pua`

### Codex（AGENTS.md）

複製 `platforms/codex/AGENTS.md` 到以下任一位置：

```bash
# 全域（所有專案生效）
cp platforms/codex/AGENTS.md ~/.codex/AGENTS.md

# 專案級（僅當前專案生效）
cp platforms/codex/AGENTS.md ./AGENTS.md
```

放入後自動生效，無需額外啟動。

### Cursor（Rules）

複製 `platforms/cursor/pua.mdc` 到專案的 `.cursor/rules/` 目錄：

```bash
mkdir -p .cursor/rules
cp platforms/cursor/pua.mdc .cursor/rules/pua.mdc
```

設定為 `alwaysApply: true`，放入後自動生效。

## 核心機制

### 三條鐵律

1. **窮盡一切** — 沒有窮盡所有方案前，禁止說「我無法解決」
2. **先做後問** — 先用工具自行排查，確實缺少資訊才提問，且必須附帶已查到的證據
3. **主動出擊** — 端到端交付，發現問題主動擴展排查範圍

### 壓力升級（自動觸發）

AI 反覆失敗時自動升級壓力等級：

| 次數 | 等級 | 強制動作 |
|------|------|---------|
| 第 2 次 | L1 溫和失望 | 切換本質不同的方案 |
| 第 3 次 | L2 靈魂拷問 | 搜尋報錯 + 讀原始碼 + 3 個不同假設 |
| 第 4 次 | L3 績效考核 | 方法論全步驟逐項工具驗證 + 3 個全新假設 |
| 第 5 次+ | L4 畢業警告 | 拼命模式：最小 PoC + 隔離環境 + 換技術棧 |

### 使用者觸發詞（手動施壓）

除了自動升級，你也可以用關鍵詞主動對 AI 施壓：

| 關鍵詞 | 對應失敗模式 |
|--------|-------------|
| 好爛、垃圾、敷衍 | 💩 品質爛 |
| 放棄吧、算了、做不到 | 🚪 放棄推鍋 |
| 又錯了、還是錯、一樣的問題 | 🔄 卡住打轉 |
| 你有查嗎、用猜的嗎 | 🔍 沒搜就猜 |
| ???（連續 3 個以上 `?`） | 🔄 卡住打轉 |

**觸發規則：** 訊息中任意位置包含關鍵詞即觸發。首次觸發直接從 L2 起跳（使用者開口代表已經不滿），同類關鍵詞重複說會繼續升級（L3 → L4），不同類別各自計數。

### 11 種 PUA 風格

依失敗模式自動選擇對應企業文化風格：

| 風格 | 語氣 |
|------|------|
| 🟠 Alibaba | 冷靜失望主管 — 底層邏輯、抓手、閉環 |
| 🟡 ByteDance | 直球對決 — Always Day 1、坦誠清晰 |
| 🔴 Huawei | 軍事化動員 — 燒不死的鳥是鳳凰 |
| 🟢 Tencent | 冷淡威脅 — 賽馬文化、只看結果 |
| 🔵 Meituan | 苦行僧激勵 — 做難而正確的事 |
| ⚫ Baidu | 嘲諷質問 — 你深度搜尋了嗎 |
| 🟣 Pinduoduo | 赤裸威脅 — 你不幹有的是人替你幹 |
| 🟤 Netflix | 冷酷專業 — Keeper Test |
| ⬛ Musk | 最後通牒 — Extremely Hardcore |
| ⬜ Jobs | 傲慢蔑視 — A players, 50x better |
| 🦁 NEU | 霸道總裁 — 狼不是牧童 |

### 通用方法論

每次失敗後強制執行五步驟：

1. **聞味道** — 列出所有嘗試，找共同模式
2. **揪頭髮** — 5 維度拉高視角（讀訊號、搜尋、讀原始碼、驗假設、反轉假設）
3. **照鏡子** — 自我檢查是否重複同思路
4. **執行新方案** — 本質不同 + 明確驗證標準
5. **複盤 + 主動延伸** — 解決後檢查同類問題

### 體面的退出

方法論全步驟完成仍未解決時，輸出結構化失敗報告，而非無限迴圈。

## 使用範例

```
你：/c2l:pua                              ← Claude Code；Codex/Cursor 自動生效
AI：⚡ C2 PUA 高效激勵引擎已啟動。...

你：幫我修這個 bug
AI：（第一次嘗試失敗）
AI：（第二次失敗 → L1 自動觸發，切換方案）

你：好爛
AI：（💩 品質爛 L2 施壓 + 重新嘗試）

你：垃圾
AI：（💩 品質爛 L3 施壓 + 載入語錄 + 重新嘗試）

你：又錯了
AI：（🔄 卡住打轉 L2 — 不同模式，獨立計數）

你：為什麼還是不對???
AI：（🔄 卡住打轉 L3 — 連續 3 個問號觸發 + 同模式第 2 次升級）
```

## 專案結構

```
.claude-plugin/
├── plugin.json              # 插件元資料（Claude Code）
└── marketplace.json         # 市集元資料（Claude Code）
commands/
└── pua.md                   # 啟動指令 /c2l:pua（Claude Code）
skills/
└── pua/
    ├── SKILL.md              # 核心邏輯（Claude Code 插件格式）
    └── references/
        └── quotes.md         # PUA 語錄庫（L3+ 載入）
platforms/
├── codex/
│   └── AGENTS.md             # 自包含版（Codex）
└── cursor/
    └── pua.mdc               # 自包含版（Cursor Rules）
```

## 各平台差異

| 特性 | Claude Code | Codex | Cursor |
|------|------------|-------|--------|
| 安裝方式 | 插件市集 | 複製 AGENTS.md | 複製 .mdc 檔案 |
| 啟動方式 | `/c2l:pua` 手動啟動 | 自動生效 | 自動生效 |
| 語錄庫 | L3+ 動態載入 | 內聯於文件底部 | 內聯於文件底部 |
| 檔案大小限制 | 無 | 32 KiB（可調） | 無硬限（建議 < 500 行） |

## 授權

MIT
