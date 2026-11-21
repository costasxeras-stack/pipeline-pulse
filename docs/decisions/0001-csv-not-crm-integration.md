# 0001: Start from a CSV export, not a CRM integration

**Status:** accepted, 0.1.0

## Context

Connecting to Salesforce or HubSpot needs an app, OAuth and a server, and each CRM is different. Every CRM can export deals to CSV.

## Decision

Version 0.1.0 takes a CSV. Column names are matched by common synonyms, and the user confirms the matching with a preview.

## Tradeoff

- Works with any CRM, today, with no setup or approval from IT.
- The review is only as fresh as the last export. A weekly export fits a weekly review.
- A later version could add one direct integration if users ask for the same CRM.
