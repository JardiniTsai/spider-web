# spider-web

[English](README.md) | [正體中文](README.zh-TW.md)

## 出處

spider-web 的核心概念取自 Felix Rieseberg 的文章〈[How to be more ambitious: A tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/)〉（發表於 2026 年 10 月 13 日）：文中的四種企圖心（Speed、Altitude、Depth、Range）、「目標之後的目標」、不合理目標、外部驗證、加深任務的四個問題、組隊與對抗角色（借做法、不扮角色），以及用原始資料挑戰既有認知。把名詞換成動詞（原文為 replace the nouns with verbs）是該文引用自 Tom Kelley 與 Jonathan Littman《The Art of Innovation》的技巧。六個階段、節點上限與交接流程是本 skill 自己加的設計，不是原作者的方法，也不代表原作者的說法；沒有暗示 Felix Rieseberg 背書。

## 用途

spider-web 是一個只能被明確呼叫的探索 skill。它先把題目框對，再把模糊的點子、任務或產品概念展開成一張「實質不同的可能性」網，讓使用者在選方向、動手之前看見整個可能性空間。它不是用來產出短清單的工具。使用者選定分枝後，會啟動 `grill-me`，只拷問選定路線；確認共識後，才可以執行。

本儲存庫提供同一個 skill 的兩個語言版本。兩者的技能名稱都是 `spider-web`，指令都是 `$spider-web`。只能安裝其中一個，不能同時安裝。

- `skills/spider-web/`：英文
- `skills/spider-web-zh/`：繁體中文（資料夾名稱可以維持 `spider-web-zh`，技能名稱仍是 `spider-web`）

**必須搭配 `grill-me` 與 `grilling` skill 使用。** 本套件不包含這兩者。`grill-me` 是啟動 `grilling` skill 的薄包裝，因此兩者都要安裝。階段 1 由本 skill 自己照 `grilling` 的問法進行（不載入該 skill）；階段 6 在寫完交接檔後直接啟動 `grill-me`，只拷問選定路線，並同時套用本 skill 的交接附加規則（含一次換枝出口）。請在同一套 agent 環境裡另行安裝名稱為 `grill-me` 與 `grilling` 的 skill。可參考 [Matt Pocock 的 skills 儲存庫](https://github.com/mattpocock/skills)（[grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)、[grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)）。

安裝本 skill 的 agent 請依 [AGENTS.md](AGENTS.md) 處理依賴與驗證。

## 六個階段

以下流程取自 skill 的 `SKILL.md`，未另行改寫。繁中版：

```
明確呼叫 spider-web
  → 階段 1：定框拷問（spider-web 自己照 grilling 的問法跑，最多 5 題，只問題目）
  → 階段 2：骨架網（全部列出 → 分群，不刪；上限 30 個節點）
  → 階段 3：使用者圈選要深挖的節點（上限 5 個）
  → 階段 4：深展開（只對圈選節點填 13 欄）
  → 階段 5：使用者選定分枝 → 產出 handoff.md
  → 階段 6：寫完交接檔後直接啟動 grill-me，只拷問選定路線（spider-web 的交接附加規則同時生效，含一次換枝出口）
  → 使用者確認共識後才執行
```

每個階段結束時，agent 會用一句話說明現在在哪個階段、下一步是什麼。每次執行的檔案放在工作區的 `spider-web-runs/<YYYYMMDD>-<短題目>/`（兩個語言版本都用同一條規則）。階段 1 結束就建立資料夾並開始寫 `web.md`，之後每個階段都更新它；階段 5 再寫 `handoff.md`。

## 安裝

1. 先在同一個 agent 環境安裝 `grill-me` 與 `grilling` skill（資料夾或技能名稱需分別為 `grill-me`、`grilling`）。細節見 [AGENTS.md](AGENTS.md)。
2. 把 `skills/spider-web` 或 `skills/spider-web-zh` 其中一個複製到該 agent 的 skills 目錄。若 loader 依資料夾名稱識別 skill，請把安裝後的資料夾命名為 `spider-web`。根目錄必須有 `SKILL.md`。不要兩個都裝。
3. 若環境會讀取 `agents/openai.yaml`，其中的 `allow_implicit_invocation: false` 會關閉隱式呼叫。即使環境不讀這個檔，skill 的 frontmatter 與內文仍規定：只有使用者明確寫出 `$spider-web` 才啟動。

不同 agent 的 skills 目錄位置不同，請依你使用的 agent 文件來安裝，不要假設特定機器或帳號路徑。

啟動方式範例（兩個語言版本的指令都是 `$spider-web`）：

```text
$spider-web 我想做……先展開可能性，不要執行。
```

或在安裝英文版時：

```text
$spider-web I want to… first expand the possibilities, don't execute.
```

只寫「幫我想幾個方向」這類說法不會啟動本 skill。

## 授權

本專案以 MIT License 授權，詳見 [LICENSE](LICENSE)。
