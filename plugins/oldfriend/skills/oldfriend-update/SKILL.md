---
name: oldfriend-update
description: Use when the user asks to update or upgrade OldFriend, asks which OldFriend version they have, or asks what changed in a new version. Manual, step by step.
---

# OldFriend update (beta, manual)

Instructions are for you, the assistant. Text in 「」 and "" is what you show the user: send the version in the user's language (zh-TW for Chinese, English otherwise).

Updates in v0.x are manual: you guide, the user confirms each step. Fetch or replace files only as the steps below say.

## 0. Rules and owner check
- Read `oldfriend/core/rules.md` and `oldfriend/me/` first and follow them. If `core/rules.md` is missing, follow these until it is restored: ask about work, plans and preferences only, talk about feelings only after the user brings them up, and on any sign of crisis or self-harm follow `oldfriend-care` right away.
- Before every write in this skill (backup, refresh, restore), read `oldfriend/VERSION` and check that its `bot:` line names you. If it names another assistant, stop and say: 「這份 OldFriend 記憶屬於「NAME」。要接手，請先執行 oldfriend-setup 的交接。」 / "This OldFriend memory belongs to "NAME". To take it over, run the handoff in oldfriend-setup first."

## 1. Show the version
- Read `oldfriend/VERSION` and report it: 「你目前的 OldFriend 版本是 X。」 / "Your OldFriend version is X."
- If `VERSION` is missing, point to `oldfriend-setup` and stop.
- Link the changelog: https://github.com/oldfriend-ai/oldfriend/blob/main/CHANGELOG.md
  「新版內容在這裡，看完決定要不要更新。」 / "Here's what's new. Decide after reading."

## 2. Back up memory (before anything else)
On the user's go-ahead, copy `oldfriend/me/` to `oldfriend/me.bak-YYYY-MM-DD/` (today's date; add `-2`, `-3` if it exists). Check the copy has the same files, then report: 「已備份你的記憶到 me.bak-YYYY-MM-DD/。」 / "Backed up your memory to me.bak-YYYY-MM-DD/."

## 3. Update the package
- **Claude Code**: the OldFriend marketplace is pinned to one release tag, so a new version means re-adding it at the new tag. Ask the user to run in a terminal:
  1. `claude plugin marketplace remove oldfriend` (this removes the plugin; the `oldfriend/` memory folder stays as it is)
  2. `claude plugin install oldfriend --marketplace oldfriend-ai/oldfriend#<new tag>` (for Claude Code older than 2.1.292, follow the Claude Code steps in that tag's `INSTALL.md`)
  3. `claude plugin list`, and check that `oldfriend@oldfriend` shows the new version. Then restart Claude Code.
- **Grok Bot**: ask the user to paste the install prompt for that tag from the README. Once a template is published, re-adding the OldFriend Bot template from the tagged release also works. Skills are rebuilt by the host.
- **Other agents** (`host: other`): upgrades are unsupported in v0.1. Point the user to the Upgrades section of `INSTALL.md` and stop.

## 4. Refresh core
After the package is updated, run `oldfriend-setup` with `refresh`. It asks consent, replaces only `oldfriend/core/` and `VERSION`, and keeps `me/`.

## 5. Check
- Read `VERSION` and report old → new.
- Confirm `me/corrections.md` still has its lines: 「更新完成：X → Y，你的記憶和更正都還在。」 / "Update done: X → Y. Your memory and corrections are all here."

## Restore
If anything in `me/` looks wrong, offer to restore: copy files back from the newest `me.bak-YYYY-MM-DD/` into `me/` after the user confirms. Keep the backup folder until the user asks to remove it.
