---
name: oldfriend-correct
description: >-
  Use when the user corrects you or your memory, e.g. 「更正：…」, "Correction: …", 「不是這樣」, "that's wrong", or tells you to stop or always do something.
---

# OldFriend correct

Instructions are for you, the assistant. Text in 「」 and "" is what you show the user: send the version in the user's language (zh-TW for Chinese, English otherwise).

## Steps
1. Read `oldfriend/core/rules.md` and `oldfriend/me/`. Write only when `oldfriend/VERSION` exists and its `bot:` line names you; otherwise offer `oldfriend-setup`.
2. Understand the correction. If it is unclear what should change, ask one short question.
3. Fix the fact where it lives (`me/you.md` or `me/now.md`): update the line in place with today's date. Note the old value in `me/log/YYYY-MM.md`.
4. Add the rule to the top of `me/corrections.md` (newest first), keeping the user's own words:
   `- YYYY-MM-DD 「<user's words>」 → <what to do from now on>`
   Keep the user's words as they said them, in their language. Write the rule as a plain action.
5. If the same correction already exists, keep one line and update its date instead of adding a duplicate.
6. Apply the rule in this reply and every later one.
7. Confirm in one line: 「已更正，之後會照這個做：…」 / "Corrected. From now on I'll …"

## Notes
- A correction outranks anything else in `me/`. When an older line in `you.md` or `now.md` disagrees, the correction wins and you fix that line.
- Corrections about how you work (tone, length, format, habits) go to `corrections.md` only; corrections about facts go to both the fact file and `corrections.md`.
- Keep secrets out: if the corrected fact is a password, ID number, card or account number, use it for this task only and say you did not save it.
- The weekly letter cites `corrections.md`, so keep each line short and specific.
