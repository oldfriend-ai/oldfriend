# Grok Bot routines

OldFriend v0.1 uses one routine per Bot: the weekly letter. Memory tidying runs inside it.

## OldFriend weekly letter

| Field | Value |
|---|---|
| Name | `OldFriend weekly letter` (exactly) |
| Owner | The Bot named on the `bot:` line of `/workspace/oldfriend/VERSION` |
| Trigger | Weekly, Sunday 20:00 in the user's local time by default; `oldfriend-setup` step 7 asks whether to keep it or change it |
| Skills used | `oldfriend-letter` (and `oldfriend-care` if needed) |
| Notifications | The host's default for routines |

### Instructions (exact text)
```
Read `oldfriend/core/rules.md` and `oldfriend/me/`, then follow the `oldfriend-letter` skill.
```

### What a run does
1. Reads the rules and the user's memory. The Bot's standing memory rule asks for the same read at the start of every routine.
2. Checks `oldfriend/VERSION`. When it is missing or names another Bot, the run sends one line pointing to `oldfriend-setup` and ends.
3. Tidies memory as `oldfriend-letter` describes: confirmed finished items move to `me/log/YYYY-MM.md`, `me/now.md` stays at 60 lines or fewer, duplicate lines in `me/you.md` are merged.
4. Sends the letter in the user's language, with up to four sections: what was noted, corrections followed, what is coming up, up to three patterns to confirm.
5. Appends `- YYYY-MM-DD HH:mm weekly letter sent` to `me/log/YYYY-MM.md`.

### Creating it
- During setup: `oldfriend-setup` step 7 is the one place that reconciles routines. It asks whether to keep Sunday 20:00 or pick another time, then looks at the Bot's routines whose names start with `OldFriend weekly letter`. On yes, it keeps one (creating it if none exists), resumes it if paused, sets the exact name, schedule and instructions above, and pauses any extra matches. On no, it pauses every match.
- Later changes: ask the Bot in chat to change the `OldFriend weekly letter` schedule. The routines (Automations) page also lets the user pause or delete it.

### In the template (future template spec)
The template, once built, carries this routine with the name and instructions above, scheduled weekly on Sunday at 20:00 in the user's local time. On first chat, setup asks whether to keep that time or change it, and updates this same routine.

### Checks for each release (see `build.md`)
- The routine runs in a separate session and applies facts and a correction found only in the files, with no chat hints.
- The letter cites a correction made earlier in chat.
- The letter contains zero unprompted questions about feelings.
