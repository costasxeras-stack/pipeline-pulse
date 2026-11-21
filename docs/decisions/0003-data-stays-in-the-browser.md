# 0003: Keep the pipeline in the browser

**Status:** accepted, 0.1.0

## Context

Deal names, amounts and owners are commercially sensitive. Uploading them to a portfolio app's server would be a reason not to use it.

## Decision

The CSV is read and stored in the browser's local storage. There is no server.

## Tradeoff

- No account, nothing to approve.
- The data lives on one device. A team sees the same view only by sharing the export or the summary.
- Very large exports may not fit in browser storage. The app says so, and still works until the page is closed.
