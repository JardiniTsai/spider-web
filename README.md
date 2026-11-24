# spider-web

**English summary.** spider-web is an agent skill that starts only when the user explicitly names it. It first frames a vague idea or task, then expands it into a web of materially distinct possibilities, and only afterwards starts `grill-me` to interrogate only the chosen path. No work is done until the user confirms a shared understanding. It is not a short-list generator. Install and use it together with both `grill-me` and `grilling`: `grill-me` is a thin wrapper that starts the `grilling` skill. See [Matt Pocock's skills repo](https://github.com/mattpocock/skills) ([grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me), [grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)). Agents installing this skill should follow [AGENTS.md](AGENTS.md).

## 用途

spider-web 是一個只能被明確呼叫的探索 skill。它先把題目框對，再把模糊的點子、任務或產品概念展開成一張「實質不同的可能性」網，讓使用者在選方向、動手之前看見整個可能性空間。

它不是用來產出短清單的工具。它的工作是攤開可能性、讓不同節點都看得見，並且在網夠廣之前不收斂。使用者選定分枝、完成拷問並確認共識後，才可以執行。

**必須搭配 `grill-me` 與 `grilling` skill 使用。** 本套件不包含這兩者。`grill-me` 是啟動 `grilling` skill 的薄包裝，因此兩者都要安裝。階段 1 由 spider-web 自己照 `grilling` 的問法進行（不載入該 skill）；階段 6 在寫完交接檔後直接啟動 `grill-me`，只拷問選定路線，並同時套用 spider-web 的交接附加規則（含一次換枝出口）。請在同一套 agent 環境裡另行安裝名稱為 `grill-me` 與 `grilling` 的 skill。可參考 [Matt Pocock 的 skills 倉庫](https://github.com/mattpocock/skills)（[grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)、[grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)）。

安裝本 skill 的 agent 請依 [AGENTS.md](AGENTS.md) 處理依賴與驗證。

## 六個階段

以下流程取自 `SKILL.md`，未另行改寫：

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

每個階段結束時，agent 會用一句話說明現在在哪個階段、下一步是什麼。每次執行的檔案放在工作區的 `spider-web-runs/<YYYYMMDD>-<短題目>/`：階段 1 結束就建立資料夾並開始寫 `web.md`，之後每個階段都更新它；階段 5 再寫 `handoff.md`。

## 安裝

1. 先在同一個 agent 環境安裝 `grill-me` 與 `grilling` skill（資料夾或技能名稱需分別為 `grill-me`、`grilling`）。
2. 把本資料夾複製到該 agent 的 skills 目錄，並保持資料夾名稱為 `spider-web`。根目錄必須有 `SKILL.md`。
3. 若環境會讀取 `agents/openai.yaml`，其中的 `allow_implicit_invocation: false` 會關閉隱式呼叫。即使環境不讀這個檔，`SKILL.md` 的 frontmatter 與內文仍規定：只有使用者明確寫出 spider-web 才啟動。

不同 agent 的 skills 目錄位置不同，請依你使用的 agent 文件來安裝，不要假設特定機器或帳號路徑。

啟動方式範例：

```text
$spider-web 我想做……先展開可能性，不要執行。
```

只寫「幫我想幾個方向」這類說法不會啟動本 skill。

## 授權

本專案以 MIT License 授權，詳見 [LICENSE](LICENSE)。
