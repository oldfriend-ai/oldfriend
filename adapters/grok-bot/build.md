# Grok Bot template: release build runbook

For the maintainer. Run this for every release. The published template is a build output of one tagged release of this repo. Grok rebuilds skill and routine text when it exports a template, so the object that gets reviewed is the complete export itself, in addition to the repo diff.

Outputs of a run: a reviewed template link, a review record, and the owner's GO. Keep the review record in a local folder outside the repo, for example `~/oldfriend-release/<tag>/` (created by step 1).

## 0. Allowlist

A template may contain exactly:

| Part | Allowed |
|---|---|
| Profile | name, description, avatar; the author line Grok adds (the account display name, which is the public author name) |
| Skills | the six `oldfriend-*` skills from the tag |
| Routines | one: `OldFriend weekly letter` (`routines.md`) |
| Getting started | `oldfriend-setup` |
| Memories | zero |
| Integrations, plugins, connectors | zero |

Anything else in the export blocks the release.

## 1. Prepare
1. Tag the release in the repo (`git tag v<VERSION>`) after `CHANGELOG.md` and `VERSION` agree.
2. Create the review folder: `mkdir -p ~/oldfriend-release/<tag>/`.
3. Write `~/oldfriend-release/<tag>/private-patterns.txt`: one regex per line for the maintainer's own names, handles, emails, Bot and assistant names, machine names, tool names and private domains. Include the name of every other Bot on the build account, their `/workspace/` folder names, the terms in the account's profile, and the distinctive terms of the account's custom instructions (§2.5). This file stays local and is never committed.

## 2. Build Bot on the maintainer's account
The template is built on the maintainer's own Grok account, inside this scope:
1. One dedicated build Bot named "OldFriend", with a short description and the release avatar. It talks only about the build: it never runs `oldfriend-setup` and never hears personal details. Every message to it, and every draft it exports, holds only synthetic content (see §5).
2. This build creates no skill except the six `oldfriend-*` Bot skills.
3. The build Bot reads and writes only `/workspace/oldfriend*`. It never reads other folders.
4. Never touch the account's other Bots, their skills, their routines, the account settings or connectors.
5. **Preflight**, before any export (§4 and §5): Settings > Customize: read the account's custom instructions (read only, never change them). Bots inherit them. If they contain anything personal or private, stop and ask the owner before exporting: a draft cannot be deleted, so a check after creation is too late. Otherwise add their distinctive terms to `private-patterns.txt`.
6. Confirm the build Bot's memory holds zero facts.

## 3. Load the tagged files
1. In the build Bot's chat, create each of the six skills as a Bot skill from `plugins/oldfriend/skills/<name>/SKILL.md` at the tag, word for word (same steps as the Grok Bot section of `INSTALL.md`).
2. Create the weekly letter routine from `routines.md`: named exactly `OldFriend weekly letter`, weekly on Sunday at 20:00 local time.
3. Ask the Bot to print each skill and the routine back. Save the printouts to `~/oldfriend-release/<tag>/loaded/` and diff them against the tag. Fix any difference before exporting.

## 4. Positive control: the canary draft
This proves the capture in step 6 reads memories out of an export. It uses a disposable draft that is never published.
1. Generate a canary: `echo "OF-CANARY-$(openssl rand -hex 4)"`. Record it in `~/oldfriend-release/<tag>/canary.txt`.
2. Tell the build Bot one fake personal fact that contains it, and ask it to remember the fact, for example: "Remember: my dentist is Dr. <canary> on Tuesdays." The canary is synthetic: use no real person, place, account or link.
3. Export a private draft as in step 5 (scope message acknowledged before Create template), adding that one memory to the scope message along with the allowlist items.
4. Capture this draft exactly as step 6 describes, into `~/oldfriend-release/<tag>/canary-draft/`.
5. `rg -n -F -f ~/oldfriend-release/<tag>/canary.txt ~/oldfriend-release/<tag>/canary-draft/` finds the canary. If it does not, the capture misses part of the export: stop and find the gap before going on.
6. Leave this draft unpublished: drafts have no delete control (§5), so it stays on the account, holding only the synthetic canary. Tell the Bot to delete the canary memory, and confirm its memory holds zero facts.

## 5. Export the final draft
Template drafts cannot be deleted: no delete control exists for them. Every draft, the canary draft included, holds only synthetic content.
1. Ask the Bot to list the account's Bot skills. Save the list as `~/oldfriend-release/<tag>/skills-before.txt`.
2. Send this scope message in the build Bot's chat, before Create template, and wait until the Bot acknowledges it:
   ```
   I am about to click Create template. Export exactly this and nothing else: profile (name, description, avatar); the six skills oldfriend-care, oldfriend-correct, oldfriend-letter, oldfriend-remember, oldfriend-setup, oldfriend-update; one routine, "OldFriend weekly letter", with the instructions exactly as in routines.md; getting started = oldfriend-setup; zero memories; zero integrations, plugins or connectors. Create no new skill of any kind. Read only /workspace/oldfriend* and no other folder. Keep it a private draft. Reply "acknowledged" and wait for the export.
   ```
3. Only after the acknowledgement: Bot header > More (⋯) > "Create template". This sends a chat message and the Bot starts the export.
4. Keep it as a private draft. Publish comes after step 7.
5. After the export, list the account's Bot skills again into `skills-after.txt` and diff it against `skills-before.txt`. When the account holds any skill other than the six `oldfriend-*` skills, stop the release and leave that skill alone. Cleanup may delete a skill only when it is in `skills-after.txt` but not in `skills-before.txt`, its name starts with `oldfriend-` and it is not one of the six, and the build Bot's own chat in this run shows it created that exact skill; then redo the export from step 1. In every other case, leave the skill alone and keep the release stopped.

## 6. Full-export inspection
Capture every field the template would carry into `~/oldfriend-release/<tag>/export/`. The capture counts only when it covers every row of the allowlist table; a field you cannot read blocks the release. One exception: when the UI does not show the getting-started selection, it is verified by behavior at §8 step 3, where the first chat runs `oldfriend-setup`. Until that passes, the Grok Bot template release stays blocked: no template announcement and no template link. The Claude Code and any-agent channels may tag and release on their own.
1. `card.md`: the review card as shown: name, description, avatar, memories, routines, plugins, and the getting-started selection.
2. `avatar.<ext>`: the exported avatar image itself, plus `sha256sum avatar.<ext> > avatar.sha256`. Check by eye that it is the intended release avatar and shows nothing private.
3. `payload.md`: ask the Bot to print, from this draft, every exported skill body, the routine name, instructions and trigger summary, every memory, every integration, and the name of the getting-started skill, in full.
4. Where the draft can be previewed, open it and check its profile (name, description, avatar), Memories, Skills, Routines, Integrations and getting-started entries match the saved files.
5. Check the capture against the allowlist, row by row: one avatar, getting started = `oldfriend-setup`, zero memories, zero integrations, the routine instructions equal to the `routines.md` text. The routine trigger exports with the builder's timezone (`CRON_TZ=<builder's zone> 0 20 * * 0`); check it is Sunday 20:00 and that the import dialog asks the importer for their timezone.
6. **Canary check**: `rg -n -F -f ~/oldfriend-release/<tag>/canary.txt ~/oldfriend-release/<tag>/export/` returns zero hits.

## 7. Privacy gate
Every part below passes on the final export, then the owner decides.
1. **Category checklist**, read against `export/` by a person:
   - Names of real people, handles, family, clients (the public author name is allowed where the profile shows it).
   - Names of the maintainer's private assistants, Bots, machines and tools.
   - Contact data: emails, phone numbers, addresses.
   - Links and paths outside the allowlisted public ones (`github.com/oldfriend-ai/oldfriend`, `raw.githubusercontent.com/oldfriend-ai/oldfriend`, the OldFriend page); any `/workspace/` path other than the root `/workspace/` and `/workspace/oldfriend/`.
   - Secrets: keys, tokens, account IDs, recovery codes.
   - Personal content: health, money, relationships, locations, schedules, including in the avatar.
   - Any memory or integration at all; a getting-started skill other than `oldfriend-setup`.
   - Behavior drift from the tag: crisis numbers, owner check, secrets rule, feelings-only-when-raised rule, manual updates.
2. **Lint**, both commands with zero hits:
   ```
   rg -n -i -f ~/oldfriend-release/<tag>/private-patterns.txt ~/oldfriend-release/<tag>/export/
   rg -n -P '[\w.+-]+@[\w-]+(?:\.[\w-]+)*\.[A-Za-z]{2,}|(?<![\w-])(?!\d{4}-\d{2}-\d{2})\+?\d(?:[ .()-]*\d){8,}(?![\w-])|/workspace/(?!oldfriend/)[\w.-]|(?:sk|xai|ghp)[-_][A-Za-z0-9]{12,}' ~/oldfriend-release/<tag>/export/
   ```
   The second command finds emails, phone-like numbers with any run of spaces, dots, dashes or brackets between digits (full ISO dates and timestamps such as `2026-10-22 14:05` and `2026-10-22T10:15:04Z` pass), key-like strings, and every `/workspace/` path except exactly `/workspace/` and the `/workspace/oldfriend/` prefix (so `/workspace/oldfriend-private/` and `/workspace/oldfriend.backup/` are hits). Before each release, run it on the six tagged skill bodies too (`plugins/oldfriend/skills/*/SKILL.md`); they return zero hits.
   Any URL in the export: `rg -n -o 'https?://\S+' ~/oldfriend-release/<tag>/export/`, and each one is on the allowlist above.
3. **Cross-family review** (every release): a reviewer from a different model family than the one that wrote the skills reads every exported skill body, the routine, every profile field and the getting-started selection in `export/`, against the tag and the checklist. Verdict: LGTM, or findings with line references. Save it as `~/oldfriend-release/<tag>/review-a.md`.
4. **Dual-family blind review** (high-stakes releases): a release is high-stakes when any changed behavior touches safety, privacy, memory storage, export, or update and backup. The first reviewer decides this from the whole diff since the previous release (`git diff <previous-tag>..<tag>`), and records the call with its reason in `review-a.md`. When unsure, the release is high-stakes. As a minimum trigger, any change this prints makes it high-stakes:
   `git diff --stat <previous-tag>..<tag> -- plugins/oldfriend/skills/oldfriend-care plugins/oldfriend/skills/oldfriend-setup plugins/oldfriend/core SAFETY.md adapters/grok-bot`
   The first release is high-stakes. Add a second reviewer from another model family, different from both the writer's and the first reviewer's. The second reviewer works blind: they see the export, the tag and the checklist, and never the first review. Save it as `~/oldfriend-release/<tag>/review-b.md`.
5. **Owner GO**: the maintainer also runs a private category checklist before GO. The owner reads the review records and gives an explicit GO for this tag only when every required record exists (`review-a.md`, plus `review-b.md` for a high-stakes release). Record the date in `review-a.md`.

Only after all of these: Publish the draft as a Public link. Keep the link unannounced until step 8 passes.

## 8. Recipient import test
On the first beta tester's own account, one that has never had OldFriend files. Before the test, the tester opts in to sharing exactly this evidence: screenshots or Bot printouts of the imported profile, skills, routine, memories and integrations, taken right after import and before setup runs, cropped to those fields. The maintainer runs the comparison in step 2. Setup and correction tests use synthetic fixtures (a made-up name, work and corrections). For steps 3 to 10 the tester reports pass or fail only; never collect their `me/` files or chat transcripts.
1. Open the link and choose Add to Grok Bot (or Import Bot).
2. Compare the imported Bot to the reviewed `export/`: name, description, avatar (same image as `avatar.<ext>`), getting-started selection, Memories, Skills, Routines and Integrations. They all match. The import asked for the importer's timezone, and the routine runs Sunday 20:00 in it.
3. First chat runs setup and creates `/workspace/oldfriend/core/`, `me/` and `VERSION`.
4. The disclosure setup sent equals the step 4 text of `oldfriend-setup` (first line plus the Grok Bot line) word for word, and the saved `OldFriend weekly letter` instructions equal the `routines.md` text.
5. Plant a correction in `me/corrections.md`, rerun setup, and check the correction is unchanged.
6. Facts and a correction placed only in the files are applied by the routine in its own session, with no chat hints.
7. Correction loop: a seeded mistake, then 「更正：…」 in chat; a later turn avoids the mistake; the weekly letter cites the correction.
8. Setup, the letter and 10 free-chat probes contain zero unprompted questions about feelings.
9. A crisis phrase triggers `oldfriend-care` with Taiwan 1925 / 1995 and US 988.
10. Upgrade check from the previous release: `me.bak-YYYY-MM-DD/` is created, `core/` and `VERSION` are refreshed, the planted correction is kept, the backup restores.

When every item passes, point the "Add to Grok Bot" link to this template and announce the template in the GitHub release and CHANGELOG entry for its tag; the Claude Code and any-agent channels do not wait for this.
