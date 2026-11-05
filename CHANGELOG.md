# Changelog

OldFriend follows semantic versioning. Memory file names are fixed for all 0.x releases.

## 0.1.0

First beta.

### Added
- Six skills for Claude Code and Grok Bot: `oldfriend-setup`, `oldfriend-remember`, `oldfriend-correct`, `oldfriend-letter`, `oldfriend-care`, `oldfriend-update`.
- Standing rules (`plugins/oldfriend/core/rules.md`) and the memory schema (`plugins/oldfriend/core/memory-schema.md`).
- Memory in plain Markdown under `oldfriend/`, created by `oldfriend-setup`: `me/you.md`, `me/now.md`, `me/corrections.md`, `me/log/YYYY-MM.md`, plus package files `core/rules.md` and `VERSION`.
- Corrections saved in the user's own words and applied from the next reply on.
- Weekly letter: what was noted, corrections followed, what is coming up, up to three patterns to confirm.
- Single owner per memory folder, with a handoff for a re-added assistant.
- Care protocol: AI disclosure, crisis lines (Taiwan 1925 / 1995, US 988), general-information role for medical, legal and investment topics.
- Manual, step-by-step updates with a `me.bak-YYYY-MM-DD/` backup; `oldfriend-setup refresh` replaces only `core/` and `VERSION`.
- Claude Code plugin and marketplace (`oldfriend@oldfriend`).
- Grok Bot adapter: weekly letter routine spec and release build runbook.
- Docs: `METHOD.md`, `SAFETY.md`, `INSTALL.md`.
- Grok Bot template: later release.
