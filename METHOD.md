# How OldFriend works

OldFriend is a set of rules and skills for an AI assistant you already use. It gives the assistant a small, plain-text memory on your own computer and a few habits for using it. The goal is simple: each week the assistant knows you a little better and repeats fewer mistakes.

This page explains the method. The exact behavior lives in the skills under `plugins/oldfriend/skills/` and the rules in `plugins/oldfriend/core/rules.md`.

## The loop

1. **Notice.** While you work together, the assistant writes down what is worth keeping: your preferences, live plans, dates, finished work.
2. **Read first.** Before any reply that uses memory, the assistant reads its rules and your memory files.
3. **Correct.** When you say 「更正：…」 or "Correction: …", the fix is saved in your words and applied from the next reply on.
4. **Review.** Once a week the assistant writes you a short letter: what it noted, which corrections it follows, what is coming up, and a few patterns it wants to confirm.
5. **Confirm.** You answer yes or no. Only what you confirm becomes a lasting fact.

Each turn of the loop is small. Over weeks it adds up to an assistant that fits how you work.

## What goes where

Everything lives in one folder, `oldfriend/`, which `oldfriend-setup` creates in the assistant's working folder. File names are fixed; the full format is in `plugins/oldfriend/core/memory-schema.md`.

| File | Holds | Example |
|---|---|---|
| `me/you.md` | Lasting facts and preferences | prefers short replies; works as a designer |
| `me/now.md` | Live threads, plans and dates (60 lines or fewer) | report due 11-03 |
| `me/corrections.md` | Your corrections in your own words, newest first | 「更正：我住台中」 → use Taichung |
| `me/log/YYYY-MM.md` | Raw notes and finished items, one file per month | 2026-10-22 14:05 sent the draft |
| `core/rules.md` | The standing rules | (package file) |
| `VERSION` | Version, which assistant owns this folder, host, setup date | (package file) |

Each fact is written once, in one place, with a date. When a fact changes, the line is updated in place and the old value goes to the log, so the history is kept without cluttering the current picture.

`now.md` stays short on purpose: it is read on every reply. Work you confirm as done or cancelled moves to the log. Active work stays visible with its real status, even when it is overdue; when space runs low, details move to the log behind a one-line pointer.

## How corrections change behavior

A correction is the strongest signal you can give.

- It is saved as one line: the date, your exact words, and the rule that follows from them.
- `corrections.md` outranks every other memory file. When an older fact disagrees with a correction, the correction wins and the older line is fixed.
- A correction about a fact updates both the fact and the corrections list. A correction about style (tone, length, format) goes to the corrections list.
- Repeating a correction refreshes its date instead of adding a duplicate.
- The weekly letter cites the corrections it applied, so you can see that each one stuck.

Your words are kept as you said them. That keeps the rule faithful to what you meant, and you can read it back any time.

## Guesses wait for your yes

The assistant records what you said or confirmed. When it notices a pattern on its own, such as "you seem to prefer bullet lists", it saves nothing yet. The pattern goes into the weekly letter as a yes/no question, and only a yes moves it into `you.md`. Memory stays a record of you, in your terms.

## The weekly letter

The letter is the review step of the loop. Before writing, the assistant tidies memory: it moves confirmed finished items to the log, keeps `now.md` within its limit, and merges duplicate lines. Then it writes up to four short sections:

1. What I noted this week
2. Corrections I now follow
3. Coming up
4. To confirm with you (at most three proposals)

The letter reports what the files show and skips empty sections. It ends with one line on how to correct anything. On Grok Bot it runs as a weekly routine at the day and time you pick; on Claude Code you run it yourself when you want it.

## Package files and your files stay apart

OldFriend keeps two kinds of files and treats them differently.

- **Package files**: `oldfriend/core/` and `oldfriend/VERSION`. Setup writes them, and an update you approve replaces them.
- **Your files**: everything in `oldfriend/me/`. Only you and your conversations change them. Updates leave them exactly as they are.

Before an update, the assistant copies `me/` to `me.bak-YYYY-MM-DD/`, so a restore is one step away. Updates run only when you start them, one confirmed step at a time.

## One folder, one owner

One computer holds one OldFriend folder. `VERSION` names the assistant that owns it, and only that assistant writes to it. If another assistant finds the folder, it explains and waits; when you re-add the same assistant, a short handoff moves ownership and keeps your memory as it is.

## Memory stays readable

- Plain Markdown, one line per item, dated. You can open, edit or delete any file yourself.
- Secrets stay out: passwords, keys, tokens, recovery codes, ID numbers, card and bank account numbers. If you share one for a task, the assistant uses it for that task and tells you it did not save it.
- Conversation stays on work, plans and preferences. The assistant talks about feelings when you bring them up, and follows your lead.

Safety and storage details are in `SAFETY.md`. Install steps are in `INSTALL.md`.
