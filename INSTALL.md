Agent: before you change anything, show the user the "What you will add" list for your host below, and wait for their OK.

# Install OldFriend

This page is written for an AI agent to read and follow. Pick the section for your host, list what you will add, wait for the user's OK, then follow the steps in order.

Everything comes from one tagged release. In the steps below, `<tag>` is the release tag the user gave you (for example `v0.1.0`). Fetch raw files from:
`https://raw.githubusercontent.com/oldfriend-ai/oldfriend/<tag>/<path>`

The six skills are:
`oldfriend-setup`, `oldfriend-remember`, `oldfriend-correct`, `oldfriend-letter`, `oldfriend-care`, `oldfriend-update`.
Each one is at `plugins/oldfriend/skills/<name>/SKILL.md`.

`oldfriend-setup` owns the memory folder. It checks for existing memory first, asks before taking any over, and creates only what is missing. Every host below hands the folder work to it.

## Claude Code

### What you will add
- The `oldfriend` plugin (the six skills) from the `oldfriend` marketplace, pinned to `oldfriend-ai/oldfriend#<tag>`.
- After setup, in the current folder: `oldfriend/VERSION`, `oldfriend/core/rules.md`, `oldfriend/me/you.md`, `oldfriend/me/now.md`, `oldfriend/me/corrections.md`, `oldfriend/me/log/YYYY-MM.md` (setup keeps any memory already there).
- One line in the current folder's `CLAUDE.md` (setup asks again before adding it).

### Steps
1. Check the version: `claude --version`.
2. Check for an earlier OldFriend marketplace: `claude plugin marketplace list`. If `oldfriend` is listed with a different source, show it to the user and ask before changing it. Removing a marketplace also removes its plugins; the `oldfriend/` memory folder stays.
3. On 2.1.292 or newer, run in a terminal:
   `claude plugin install oldfriend --marketplace oldfriend-ai/oldfriend#<tag>`
4. On older versions, run inside Claude Code:
   `/plugin marketplace add oldfriend-ai/oldfriend#<tag>`
   `/plugin install oldfriend@oldfriend`
5. Verify the installed revision:
   - `claude plugin marketplace list --json` has an entry with `"name": "oldfriend"`, `"repo": "oldfriend-ai/oldfriend"` and `"ref": "<tag>"`.
   - `claude plugin list` shows `oldfriend@oldfriend` with the version that matches the tag (`v0.1.0` → `0.1.0`).
   If either differs, stop and show the user both outputs.
6. Restart Claude Code in the folder where the user wants OldFriend to live.
7. Run `/oldfriend:oldfriend-setup` and follow it to the end.
8. Report what was installed, the verified source and version, and where the memory folder is.

## Grok Bot

Use the steps below when the user asks you, a Grok Bot, to install OldFriend in chat.

### What you will add
- Six Bot skills, created from the tagged files. Bot skills are shared by every Bot on this account.
- One standing rule in your Bot memory: "Before any reply that uses memory, and at the start of every routine, read `oldfriend/core/rules.md` and `oldfriend/me/`."
- On this Grok Bot computer: `/workspace/oldfriend/` with `VERSION`, `core/rules.md`, `me/you.md`, `me/now.md`, `me/corrections.md`, `me/log/YYYY-MM.md` (setup keeps any memory already there).
- If the user wants it: one routine, "OldFriend weekly letter", weekly on Sunday 20:00 local time or the time they pick.

Tell the user that every Bot on their account can read files on this computer and use these skills.

### Steps
1. Check your Bot skills for names starting with `oldfriend-`. If any exist, show their names and ask whether to keep or replace them.
2. Fetch the six `SKILL.md` files from the tag. Create each one as a Bot skill with the same `name`, `description` and body, word for word. Create them as your own Bot skills; skills on the grok.com Plugins page are a separate store that Bots do not read.
3. Read each new skill back and check it matches the fetched file. Report any difference.
4. Run `oldfriend-setup` from step 1 (Guard) to the end. It handles the folder, the memory rule, the disclosure, the three questions and the weekly letter routine.
5. Report the skills, the folder, the memory rule and the routine schedule.

## Any other agent

For agents without an OldFriend package (Codex and others). Your host value is `other`.

### What you will add
- The six skills: in your own skill folder if you support skills; otherwise as `oldfriend/skills/<name>/SKILL.md`.
- In your working folder, through setup: `oldfriend/VERSION`, `oldfriend/core/rules.md`, `oldfriend/me/you.md`, `oldfriend/me/now.md`, `oldfriend/me/corrections.md`, `oldfriend/me/log/YYYY-MM.md` (setup keeps any memory already there).
- One pointer line in your instruction file (for example `AGENTS.md`); setup asks again before adding it.

### Steps
1. Fetch the six `SKILL.md` files and `plugins/oldfriend/core/memory-schema.md` from the tag. Write nothing yet.
2. Run step 1 (Guard) of the fetched `oldfriend-setup`. It only reads. Follow its outcome; when it stops, you stop.
3. When the guard leads on to writing (first-time setup, a confirmed takeover, or repair), add the six skills as listed under "What you will add".
4. Continue `oldfriend-setup` from where the guard sends you, to the end. Its steps name what to do on another agent.
5. Report every file you created and the line you added.

### Upgrades
Upgrades for other agents are unsupported in v0.1, and `oldfriend-update` does not cover them. To move to a new tag:
1. Copy `oldfriend/me/` to `oldfriend/me.bak-YYYY-MM-DD/` and check the copy has the same files.
2. Reinstall from the new tag: replace the six skills (and `oldfriend/skills/` if you used it) and `oldfriend/core/rules.md` with the new tag's files, and set the first line of `oldfriend/VERSION` to the new version.
3. Keep `oldfriend/me/` exactly as it is.

## After install
- Memory and growth loop: `METHOD.md`.
- Storage, privacy and safety: `SAFETY.md`.
- Later updates on Claude Code and Grok Bot: ask the assistant to run `oldfriend-update`.
