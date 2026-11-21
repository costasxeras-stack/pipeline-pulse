# Case study: Pipeline Pulse

## The problem

Every sales team has a weekly review, and someone spends an hour before it pulling numbers out of the CRM into a spreadsheet. The CRM has the data but not the view: what came in this week, what closed, where the quarter will land, and which deals are going quiet. Most teams cannot add a BI tool for this, and a spreadsheet breaks every time the export changes.

## Approach

The hard part of tools like this is not the charts. It is getting real, messy files in without friction, and earning enough trust that people put their data in at all. So I started from the import and the privacy model, then built the views a user would check every week. The main decisions:

### 1. Start from a CSV export, not a CRM integration

Connecting to Salesforce or HubSpot needs an app, OAuth and a server, and each CRM is different. Every CRM can export deals to CSV.

**Decision:** Version 0.1.0 takes a CSV. Column names are matched by common synonyms, and the user confirms the matching with a preview.

Full record: [docs/decisions/0001-csv-not-crm-integration.md](decisions/0001-csv-not-crm-integration.md)

### 2. Forecast with stage weights the user can change

Teams forecast in different ways: rep calls, stage weights, or models trained on history. Models need more history than one export usually has.

**Decision:** Forecast = won this quarter + open deals closing this quarter × the weight of their stage. Weights start as a sensible ladder and can be edited. The page also shows the best case, every open deal closing, so the user can see the range.

Full record: [docs/decisions/0002-weighted-forecast-with-editable-weights.md](decisions/0002-weighted-forecast-with-editable-weights.md)

### 3. Keep the pipeline in the browser

Deal names, amounts and owners are commercially sensitive. Uploading them to a portfolio app's server would be a reason not to use it.

**Decision:** The CSV is read and stored in the browser's local storage. There is no server.

Full record: [docs/decisions/0003-data-stays-in-the-browser.md](decisions/0003-data-stays-in-the-browser.md)

## What it does

- **Import:** drop any CRM deals export as CSV. Commas, semicolons and tabs, European number formats and day-first or month-first dates are handled. Column names are matched automatically, and you can fix the matching with a preview before importing.
- **This week:** new pipeline, won and lost, 90-day win rate and days from created to won, each against the week before. A 12-week chart of created and won value.
- **Quarter forecast:** won so far, plus open deals expected to close this quarter weighted by stage, against your target, with a plain sentence on the gap.
- **Summary to paste:** the week in six lines, ready for the team channel.
- **Pipeline:** open value by stage with editable stage weights, expected close by month with overdue deals flagged, and win rate by source.
- **Needs attention:** open deals with no activity for a set number of days or a close date in the past, biggest first, filterable by owner.
- **Team:** open and weighted pipeline, wins this quarter, win rate and alerts per owner.
- **Sample data:** a made-up pipeline of 260 deals, clearly marked, to try it without a file.

## How it was tested

Every flow was clicked through on desktop and phone widths, with the made-up sample data and with test files built to be awkward: semicolons, European number formats, lines above the header and rows with missing values. Problems found and fixed before release included stage weights carried over from the sample into an import, and charts and tables that did not fit on a phone.

## What I would measure

No usage data yet, so there are no findings. These are hypotheses to test with real users.

| Measure | Definition | Target |
|---|---|---|
| Time saved | Minutes spent preparing the weekly review, before and after | [x] min |
| Weekly use | Share of weeks with at least one import | [x]% |
| Forecast accuracy | Weighted forecast at week 6 against the quarter's actual result | [x]% |

## What I would do next

1. A direct HubSpot or Salesforce import
2. Stage weights learned from the team's own history
3. Week-over-week change per deal: what moved stage, what slipped

## My role

I defined the problem, the users, the features and the decisions, and tested every flow. Claude (Anthropic) wrote the code with me. The idea started from an example in Justin McKelvey's list of vibe coding projects, which I turned into a full app with my own product choices.
