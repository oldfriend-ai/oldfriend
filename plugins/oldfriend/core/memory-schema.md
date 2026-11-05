# OldFriend memory schema (v0.1.0)

All memory is plain Markdown on the user's own computer. File names are fixed for v0.x.

## Location
- Grok Bot: `/workspace/oldfriend/`
- Claude Code: `./oldfriend/` in the folder where the user runs it
- Other agents: `oldfriend/` in the agent's working folder
- One OldFriend folder per computer.

## Layout
| Path | Owner | Holds |
|---|---|---|
| `oldfriend/VERSION` | package | version, current assistant, host, setup date |
| `oldfriend/core/rules.md` | package | standing rules; replaced on update |
| `oldfriend/skills/<name>/SKILL.md` | package | optional: the six skills, for agents without native skills; package-owned, like `core/` |
| `oldfriend/me/you.md` | user | lasting facts and preferences |
| `oldfriend/me/now.md` | user | live threads, plans, dates; 60 lines or fewer |
| `oldfriend/me/corrections.md` | user | corrections in the user's words, newest first |
| `oldfriend/me/log/YYYY-MM.md` | user | raw notes, append only, one file per month |
| `oldfriend/me.bak-YYYY-MM-DD/` | user | copy of `me/` made before an update |

The package writes `core/`, `VERSION` and, when present, `skills/`. Updates never overwrite `me/`.

## VERSION
```
oldfriend 0.1.0
bot: <assistant name>
host: grok-bot | claude-code | other
setup: YYYY-MM-DD
```
On Claude Code, `bot:` is `claude-code`.

## Line formats
- `you.md`, `now.md`: `- <fact> (YYYY-MM-DD)` under a heading.
- `corrections.md`: `- YYYY-MM-DD 「<user's words>」 → <what to do from now on>`
- `log/YYYY-MM.md`: `- YYYY-MM-DD HH:mm <note>`

## Never stored
Passwords, keys, tokens, recovery codes, ID numbers, card and bank account numbers.

## Templates

`me/you.md`
```
# You

## Name and how to address you

## Work and projects

## Preferences
```

`me/now.md`
```
# Now
<!-- Live threads, plans and dates. 60 lines or fewer; finished items move to log/. -->

## In progress

## Coming up
```

`me/corrections.md`
```
# Corrections
<!-- Newest first. - YYYY-MM-DD 「the user's words」 → what to do from now on -->
```

`me/log/YYYY-MM.md`
```
# Log YYYY-MM
```
