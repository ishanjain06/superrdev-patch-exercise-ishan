# Patch Exercise Notes

## Summary

Fixed two high-value issues found during testing:

1. Fixed the H2 in-memory database lifecycle issue that caused the `tasks` table to become unavailable and resulted in HTTP 500 errors when loading tasks. Added `DB_CLOSE_DELAY=-1` to the H2 datasource URL so the database remains available while the application is running.

2. Fixed the task search/status filtering query. The original SQL had incorrect `AND`/`OR` precedence, causing archived tasks and tasks with other statuses to appear in filtered results. Added parentheses around the title/description search conditions and kept the optional status filter correctly grouped.

## What I Did Not Change

I did not change the frontend filtering implementation or add persistence of filter selections across page refreshes. The filtering behavior itself works correctly, and persisting UI state was considered lower priority for the exercise timebox.

I also did not rewrite the existing architecture or unrelated code.

## Biggest Remaining Risk

The application still uses an in-memory H2 database, so data is not persistent across application restarts. This was intentionally left unchanged because the exercise focuses on targeted fixes rather than changing the database architecture.

## Tools / AI Used

Used VS Code, PowerShell, browser DevTools, Maven, and API/browser testing during debugging. Used ChatGPT for debugging assistance, SQL reasoning, and understanding the existing code. All fixes were reviewed and tested locally.