---
name: oldfriend-letter
description: >-
  Use for the OldFriend weekly letter: when the weekly routine runs, or when the user asks for 週報/每週信/weekly letter/what you noted this week.
---

# OldFriend weekly letter

Instructions are for you, the assistant. Text in 「」 and "" is what you show the user: write the letter in the user's language (zh-TW for Chinese, English otherwise).

## Read first
- Read `oldfriend/core/rules.md`, `me/you.md`, `me/now.md`, `me/corrections.md`, and this month's `me/log/YYYY-MM.md` (plus last month's if the week spans both).
- Run only when `oldfriend/VERSION` exists and its `bot:` line names you; otherwise send one line pointing to `oldfriend-setup` and stop.

## Tidy memory (before writing)
- Move items the user confirmed done or cancelled from `now.md` to `log/YYYY-MM.md`, with that status.
- Keep overdue active work in `now.md` with its real status (e.g. `overdue since 10-20`), and list it under 「接下來」 / "Coming up".
- Keep `now.md` at 60 lines or fewer as `oldfriend-remember` describes: compact active items, move their detail to `log/` with a one-line pointer, or move a group to the dated `Active backlog` section in `log/YYYY-MM.md` behind one pointer line. Never mark work done to make room.
- Merge duplicate lines in `you.md`. Leave the user's facts and corrections as they are.

## Write the letter
Plain, short, about work and life admin. Use these four sections, each with 1–5 bullets; skip a section that has nothing.

1. 「這週記下的事」 / "What I noted this week": new facts, finished work and decisions from `log/` and `now.md`, with dates.
2. 「我正在遵守的更正」 / "Corrections I now follow": cite each correction added or applied this week as `YYYY-MM-DD 「user's words」 → rule`, and one line on where you applied it.
3. 「接下來」 / "Coming up": dates and open threads from `now.md` for the next 1–2 weeks, plus the items in the `Active backlog` section of `log/` with their status.
4. 「想跟你確認」 / "To confirm with you": at most 3 patterns you noticed yourself, each as a yes/no proposal, e.g. 「你好像偏好條列，要我記下來嗎？」 / "You seem to prefer bullet lists. Should I remember that?" Save one to `you.md` only after the user says yes.

Close with one line: 「有要更正的，回覆「更正：…」就好。」 / "To correct anything, reply "Correction: …"."

## Keep it factual
- Report what the files show. When a section is empty, leave it out rather than filling it.
- Ask about work, plans and preferences only. Leave feelings to the user: respond to them when they bring them up, and follow `oldfriend-care` for crisis signals.
- Leave secrets out of the letter, even if an old line contains one; remove that line from memory and mention it.

## After sending
Append to `me/log/YYYY-MM.md`: `- YYYY-MM-DD HH:mm weekly letter sent`.
