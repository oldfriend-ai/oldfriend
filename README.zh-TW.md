[English](README.md)

# OldFriend 老朋友

**與你成長的 AI**

記得你的喜好，陪你一路把事做好

<!-- STORY: Penchan's words. Edit here. -->
## 為什麼做這個

這個專案對我的意義非比尋常，可以說是我最重要的專案。我一直覺得，AI agent 是長期一起做事的夥伴，而不是用完即丟的工具。

我從 2026 年 1 月開始實驗，1 月 31 日第一次用開源 agent，之後每天都和它一起工作。我希望我的 AI agent 從第一次接觸開始，慢慢走進生活的各個面向，一起把事情做好。

OldFriend 是我把這套做法整理出來、免費分享的第一步。
<!-- /STORY -->

## OldFriend 是什麼

一套免費開源的記憶和做事工具，裝在你已經在用的 AI 助理上：Claude Code、Grok Bot 或其他 agent。它是一組規則和技能（skills），在助理的電腦上留一份純文字記憶，用你的原話記下更正，每週寫一封信給你。我們不架設任何服務，你也不用跟我們註冊帳號。

### 記得你的喜好

長期的偏好和事實寫進 `me/you.md`。進行中的事和日期寫進 `me/now.md`，最多 60 行。零碎紀錄按月寫進 log。每件事只寫一次，都附上日期。

### 照你的更正做

說「更正：…」，它會用你的原話記下來，下一句回覆就照新的做。更正的優先順序高於其他所有記憶。

### 每週一封信

信裡整理這週記下的事、它正在遵守的更正、接下來的安排，最多再提三個它觀察到的習慣，問你對不對。你說對，才會存成長期記憶。Grok Bot 在設定時可以開啟每週信，預設週日 20:00，時間可以自己選。Claude Code 隨時輸入 `/oldfriend:oldfriend-letter` 就有。

### 檔案在你手上

全部是純文字 Markdown，你隨時可以打開、修改或刪除。更新只換套件本身的檔案，動手前會先備份你的記憶。

完整的運作方式在 [METHOD.md](METHOD.md)。

## 接下來的方向

v0.1 是地基。我希望 agent 慢慢做到下面四件事，這一版做到哪裡也一起標出來：

1. **有自己沉澱的時間**：回頭整理對你的了解，歸納你的喜好。v0.1：每週信會整理記憶，和你一起回顧它注意到的事。
2. **自己反思、自己學習**：從對話裡學，慢慢長出自己的個性。v0.1：你的更正和確認過的偏好，下一句就生效。個性留到之後的版本。
3. **能做事**：例如指揮其他 agent。v0.1：幫你記著進行中的事、計畫和日期。指揮其他 agent 留到之後的版本。
4. **在這些基礎上創造**：自己找到更多能做的事，主動跟你提案，帶來新發現。v0.1：它推測出你的偏好時，會在工作中或每週信裡先問你。自己發現新的事、主動跟你提案，留到之後的版本。

## 安裝

### Claude Code（2.1.292 以上）

在終端機執行：

```
claude plugin install oldfriend --marketplace oldfriend-ai/oldfriend#v0.1.0
```

較舊的版本，改在 Claude Code 裡輸入：

```
/plugin marketplace add oldfriend-ai/oldfriend#v0.1.0
/plugin install oldfriend@oldfriend
```

設定前，先確認 `claude plugin list` 顯示 `oldfriend@oldfriend` 版本 0.1.0。之前裝過的話，請照 [INSTALL.md](INSTALL.md) 的檢查步驟做。

接著在你想放 OldFriend 的資料夾重新啟動 Claude Code，再輸入 `/oldfriend:oldfriend-setup`。

### Grok Bot、Codex 和其他 agent

把這段貼給你的助理：

```
請讀 https://raw.githubusercontent.com/oldfriend-ai/oldfriend/v0.1.0/INSTALL.md，安裝 OldFriend v0.1.0。先列出你會新增的規則和檔案，等我同意後再照做。
```

OldFriend 是免費套件。在 Grok Bot 上安裝，需要符合資格的 [Grok Bot 方案](https://docs.x.ai/grok-bot/get-started)。之後會推出按一下就能加入 Grok Bot 的範本。

各平台的詳細步驟在 [INSTALL.md](INSTALL.md)。

## 記憶存在哪裡

- **Claude Code**：你執行 Claude Code 那個資料夾裡的 `./oldfriend/`。經你同意，設定時會在該資料夾的 `CLAUDE.md` 加一行，讓助理每次都先讀你的記憶。
- **Grok Bot**：Grok Bot 電腦上的 `/workspace/oldfriend/`。這台電腦在服務商的雲端上，由你帳號裡的所有 Bot 共用，所以**你帳號裡的每個 Bot 都讀得到你的 OldFriend 記憶。**
- **其他 agent**：放在 agent 的工作資料夾，並在它的指令檔加一行指引，兩者都會先列給你同意。

OldFriend 專案不架設任何服務，也收不到你的任何資料。你的對話由你所用助理的服務商依其條款處理。密碼、金鑰、權杖（token）、復原碼、身分證號、卡號和銀行帳號都不會存進記憶。

模型訓練：在 Grok Bot 上，會不會拿資料做模型訓練，取決於這個 Bot 所用帳號的隱私設定。請到那裡關閉模型訓練。最新說明請看服務商的 [Grok Bot 隱私說明](https://docs.x.ai/grok-bot/approvals-security-and-privacy)。Claude Code 的模型訓練設定在你 Claude 帳號的隱私設定裡。

## 它不做的事

- **不會自動更新。** 每次更新都由你開始：助理先備份記憶，再一步一步帶你做，每一步都等你確認。
- **不做諮商或心理治療。** 它幫你記事、把事做好。需要諮商時，請找合格的專業人員。
- **醫療、法律、投資只提供一般資訊。** 實際決定請交給醫師、律師或合格的理財顧問。
- **不登入帳號、不購買、不付款。** 它的技能讀寫 `oldfriend/` 資料夾、和你對話。設定時還會加一個指向記憶的指引：在 Claude Code 和其他 agent 上，經你同意，在助理的指令檔加一行。在 Grok Bot 上，在 Bot 記憶存一條規則，你想要的話再加一個每週信的例行任務。

## 使用前先知道

- OldFriend 跑在 AI 上，不是真人。設定時會說明，你問的時候也會說明。
- 適用 18 歲以上。
- 它聊工作、計畫和偏好。感受的話題，等你先提起才會談。
- 這些規則和技能用來引導助理，它還是可能出錯，重要的事請自己再確認。
- 對話出現危機訊號時，它會立刻給你求助專線（安心專線 1925、生命線 1995，美國 988）。完整說明在 [SAFETY.md](SAFETY.md)。

## 常見問題

**要錢嗎？**
OldFriend 免費，採 MIT 授權。助理本身的方案照各家規定。

**可以自己改記憶嗎？**
可以。直接打開 `oldfriend/me/` 裡的檔案，或跟它說「更正：…」。

**兩個助理可以共用一份記憶嗎？**
一台電腦只放一份 OldFriend，由 `oldfriend/VERSION` 記名的助理負責寫入。別的助理找到這個資料夾，會先說明、等你決定。重新加入同一個 Bot 時，回覆「交接」就能接手，記憶原樣保留。

**怎麼更新？**
在 Claude Code 或 Grok Bot 上，請助理執行 `oldfriend-update`。它會先把記憶複製到 `me.bak-YYYY-MM-DD/`，需要時一步就能還原。其他 agent 請看 [INSTALL.md](INSTALL.md) 的 Upgrades 段落。

## 說明文件

[METHOD.md](METHOD.md) · [INSTALL.md](INSTALL.md) · [SAFETY.md](SAFETY.md) · [CHANGELOG.md](CHANGELOG.md)

OldFriend 是獨立的開源專案，和 Anthropic、xAI/SpaceXSI、OpenAI 都沒有合作關係，也未獲得它們背書。Claude 是 Anthropic 的商標，Grok 是 xAI/SpaceXSI 的商標，Codex 是 OpenAI 的商標。

---

By Penchan P · [MIT 授權](LICENSE)
