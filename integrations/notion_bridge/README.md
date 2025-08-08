# Notion ↔ Jarvis Bridge

Jarvis (sandboxed) writes requests into notion_queue.ftai.
Claude watches, executes in Notion, and logs results to notion_updates.ftai.

## Flow
1. Jarvis writes request (status=pending) into the queue.
2. Claude polls the repo on a schedule.
3. Claude executes request in Notion.
4. Claude appends the outcome to notion_updates.ftai.
5. Claude marks the queue entry as done.

## Supported Actions (MVP)
- create_page
- update_page
- append_block
- upsert_db_row

## Safety
- Never edit past result blocks.
- On error: log outcome=failure, include error message, retry up to 2x.

## Purpose

Two-way communication between Jarvis and Notion without exposing API tokens to Jarvis.