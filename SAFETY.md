# Safety and privacy

[English](#english) · [繁體中文](#繁體中文)

## English

These are instructions the assistant follows. It can still make mistakes, so they are not a guarantee.

### It is an AI
OldFriend runs on an AI assistant. It is not a person. It says so at setup, whenever you ask, and whenever a conversation treats it as human. It works alongside you on work and life admin, and it encourages time with the people in your life.

### If you are in crisis
If you are thinking about hurting yourself, or you are in danger, please reach a real person now:
- Taiwan: 安心專線 **1925** (24 hours) · 生命線 **1995** · emergency **119** / **110**
- United States: call or text **988** (Suicide & Crisis Lifeline) · emergency **911**
- Elsewhere: your local emergency number

When a conversation shows crisis signs, the assistant follows the `oldfriend-care` skill: it responds right away, gives these numbers, asks whether you are safe, and reminds you that it is an AI and cannot call anyone or send help.

### Adults only
OldFriend is for people 18 and older.

### General information only
OldFriend shares general information and helps you prepare questions. Medical, legal and investment decisions belong with a qualified professional: a doctor, a lawyer, or a licensed financial adviser. For urgent symptoms, contact emergency services first.

### What it stores and where
- **Memory**: plain Markdown files in an `oldfriend/` folder that setup creates on the computer your assistant works on. `METHOD.md` lists every file. You can open, edit or delete them any time.
- **Grok Bot**: the folder is `/workspace/oldfriend/` on your Grok Bot computer. That computer runs in the provider's cloud, and every Bot on your Grok account shares it, so **every Bot on your account can read your OldFriend memory.** Setup also saves one standing rule to the Bot's memory, telling it to read the OldFriend files.
- **Claude Code**: the folder is `./oldfriend/` in the folder where you run Claude Code. With your OK, setup adds one line to that folder's `CLAUDE.md` so the assistant reads your memory each time.
- **Other agents**: the folder sits in the agent's working folder, plus one pointer line in its instruction file, both listed for your OK before install.
- **Kept out of memory**: passwords, keys, tokens, recovery codes, ID numbers, card and bank account numbers.
- **The OldFriend project hosts nothing and receives none of your data.** Your conversations and files are handled by your assistant's provider under that provider's terms.
- **Beta testers, by choice**: a tester who opts in shares screenshots of the imported Bot's profile, skills, routine, memories and integrations, taken before setup, plus pass or fail results. Their memory files and chats are never collected.

### Model training
On Grok Bot, training opt-out follows the privacy settings of the account your Grok Bot uses. Turn model training off there. The provider's Grok Bot [approvals, security and privacy](https://docs.x.ai/grok-bot/approvals-security-and-privacy) page has the current details.
On Claude Code, model training is set in your Claude account's privacy settings.

### What OldFriend does
- **Updates when you ask.** Every update is manual: the assistant backs up your memory, then guides you one confirmed step at a time.
- **A work assistant.** It helps you remember and get things done. For counseling or therapy, please see a licensed professional.
- **Memory and conversation.** OldFriend's skills read and write the `oldfriend/` folder and talk with you. Setup also adds one pointer to your memory: on Claude Code and other agents, with your OK, one line in the assistant's instruction file; on Grok Bot, one rule in Bot memory, plus a weekly letter routine if you want one. They add no account sign-ins, purchases or payments.

## 繁體中文

這些是助理遵循的指示，它仍可能出錯，不代表保證。

### 這是 AI
OldFriend 跑在 AI 助理上，不是真人。設定時會說明，你問的時候會說明，對話把它當成真人時也會說明。它陪你處理工作和生活上的事，也鼓勵你多和身邊的人相處。

### 如果你現在很難受
如果你有傷害自己的念頭，或正處在危險中，請現在就找真人談談：
- 台灣：安心專線 **1925**（24 小時）· 生命線 **1995** · 緊急危險 **119** / **110**
- 美國：撥打或傳訊 **988**（Suicide & Crisis Lifeline）· 緊急 **911**
- 其他地區：當地緊急電話

對話出現危機訊號時，助理會照 `oldfriend-care` 技能處理：立刻回應、給你上面的電話、問你現在是否安全，並提醒你它是 AI，沒辦法幫你打電話或派人過去。

### 僅限成人
OldFriend 適用 18 歲以上。

### 只提供一般資訊
OldFriend 提供一般資訊，幫你整理想問的問題。醫療、法律和投資的決定，請交給合格的專業人士：醫師、律師或合格的理財顧問。症狀緊急時，請先聯絡緊急救護。

### 存了什麼、存在哪裡
- **記憶**：純文字 Markdown 檔，放在設定時於助理所用電腦上建立的 `oldfriend/` 資料夾。每個檔案都列在 `METHOD.md`。你隨時可以打開、修改或刪除。
- **Grok Bot**：資料夾是 Grok Bot 電腦上的 `/workspace/oldfriend/`。這台電腦在服務商的雲端上，由你 Grok 帳號裡的所有 Bot 共用，所以**你帳號裡的每個 Bot 都讀得到你的 OldFriend 記憶。** 設定時也會在 Bot 的記憶裡存一條固定規則，請它讀取 OldFriend 的檔案。
- **Claude Code**：資料夾是你執行 Claude Code 那個資料夾裡的 `./oldfriend/`。經你同意後，設定會在該資料夾的 `CLAUDE.md` 加一行，讓助理每次都先讀你的記憶。
- **其他代理**：資料夾放在代理的工作資料夾，並在它的指令檔加一行指引，安裝前都會先列給你同意。
- **不會存進記憶的**：密碼、金鑰、權杖（token）、復原碼、身分證號、卡號和銀行帳號。
- **OldFriend 專案不架設任何服務，也收不到你的任何資料。** 你的對話和檔案由你所用助理的服務商依其條款處理。
- **Beta 測試者自願提供**：同意參與的測試者，會分享匯入後、設定前的 Bot 截圖（個人檔案、技能、例行任務、記憶和整合），以及每項測試通過與否。我們不會收集測試者的記憶檔或對話。

### 模型訓練
在 Grok Bot 上，會不會拿資料做模型訓練，取決於這個 Bot 所用帳號的隱私設定。請到那裡關閉模型訓練。最新說明請看服務商的 Grok Bot [approvals, security and privacy](https://docs.x.ai/grok-bot/approvals-security-and-privacy) 頁面。
在 Claude Code 上，模型訓練的設定在你 Claude 帳號的隱私設定裡。

### OldFriend 做什麼
- **你說要更新才更新。** 每次更新都是手動：助理先備份你的記憶，再一步一步帶你做，每一步都等你確認。
- **做事的助理。** 它幫你記事、把事做好。需要諮商或心理治療時，請找合格的專業人員。
- **處理記憶和對話。** OldFriend 的技能讀寫 `oldfriend/` 資料夾、和你對話。設定時還會加一個指向記憶的指引：在 Claude Code 和其他助理上，經你同意，在助理的指令檔加一行；在 Grok Bot 上，在 Bot 記憶存一條規則，你想要的話再加一個每週信的例行任務。不會加上任何帳號登入、購買或付款功能。
