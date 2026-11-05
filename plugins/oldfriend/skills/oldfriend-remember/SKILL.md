---
name: oldfriend-remember
description: Use when the user says 記住/remember, shares a lasting preference or fact, starts or finishes a piece of work, or mentions a plan or date worth keeping in OldFriend memory.
---

# OldFriend remember

Instructions are for you, the assistant. Text in 「」 and "" is what you show the user: send the version in the user's language (zh-TW for Chinese, English otherwise).

## Before writing
- Read `oldfriend/core/rules.md` and `oldfriend/me/`.
- Write only when `oldfriend/VERSION` exists and its `bot:` line names you. Otherwise say: 「OldFriend 還沒設定，要現在設定嗎？」 / "OldFriend isn't set up yet. Set it up now?" and use `oldfriend-setup` on yes.

## Where it goes
| What | File | Example |
|---|---|---|
| Lasting facts and preferences | `me/you.md` | prefers short replies; works as a designer |
| Live threads, plans, dates | `me/now.md` | report due 11-03; planning a trip in December |
| Raw notes and finished items | `me/log/YYYY-MM.md` | 2026-10-22 14:05 sent the draft to the client |
| Corrections | use `oldfriend-correct` | 「更正：我住台中」 |

- One line per item: `- <fact> (YYYY-MM-DD)` under the right heading; log lines are `- YYYY-MM-DD HH:mm <note>`.
- Update a line in place when the fact changed; add the old value to the log.
- Record what the user said or confirmed.
- A pattern you infer yourself (a preference, a habit) waits for the weekly letter's 「想跟你確認」 / "To confirm with you" section and goes into `me/you.md` only after the user agrees. You may also ask the user right away.
- A short note for the task at hand may carry `(guess)` in `me/now.md` or `log/`. `me/you.md` holds confirmed facts only.
- Write the same fact once. Check `me/` for an existing line before adding.

## Keep now.md short
- `now.md` stays at 60 lines or fewer.
- Move an item to `log/YYYY-MM.md` only when the user confirmed it done or cancelled; record that status.
- Overdue active work stays in `now.md` with its real status, e.g. `- report (due 10-20, overdue, in progress)`.
- When `now.md` would pass 60 lines with active work: merge related items into shorter lines, or move an item's detail to `log/YYYY-MM.md` and keep one line in `now.md`: `- <item> (active; detail in log/YYYY-MM.md)`.
- If that still leaves more than 60 lines: move the oldest or least urgent active items as a group to a `## Active backlog` section in `log/YYYY-MM.md` (with `Updated: YYYY-MM-DD` on the line below the heading), keeping each item's status and dates. Put one line in their place in `now.md`: `- (N more active items: log/YYYY-MM.md#active-backlog)`. When an item there gets urgent, move it back to `now.md`.
- Never mark work done to make room.

## Secrets stay out
Never write passwords, keys, tokens, recovery codes, ID numbers, card or bank account numbers. If the user shares one, use it only for the current task and say: 「這個屬於敏感資料，我這次用完就不會存下來。」 / "That's sensitive, so I used it for this task only and did not save it."

## Confirm
- When the user asked you to remember: reply in one line with what you saved and where, e.g. 「記下了：喜歡簡短回覆（you.md）。」 / "Saved: prefers short replies (you.md)."
- When you saved on your own during other work: mention it in one short line at the end of the reply.
