# Changelog

All notable changes to this project. Versions follow [docs/versioning.md](docs/versioning.md).

## [0.1.0] - 2026-11-21

First release.

### Added
- Import: drop any CRM deals export as CSV. Commas, semicolons and tabs, European number formats and day-first or month-first dates are handled. Column names are matched automatically, and you can fix the matching with a preview before importing.
- This week: new pipeline, won and lost, 90-day win rate and days from created to won, each against the week before. A 12-week chart of created and won value.
- Quarter forecast: won so far, plus open deals expected to close this quarter weighted by stage, against your target, with a plain sentence on the gap.
- Summary to paste: the week in six lines, ready for the team channel.
- Pipeline: open value by stage with editable stage weights, expected close by month with overdue deals flagged, and win rate by source.
- Needs attention: open deals with no activity for a set number of days or a close date in the past, biggest first, filterable by owner.
- Team: open and weighted pipeline, wins this quarter, win rate and alerts per owner.
- Sample data: a made-up pipeline of 260 deals, clearly marked, to try it without a file.
