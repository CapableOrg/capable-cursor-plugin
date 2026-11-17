---
name: capable-crm
description: Use the connected Capable CRM to prepare for meetings, inspect pipeline records, or turn notes and emails into a complete review of proposed CRM changes. Applies to Capable CRM work, not unrelated coding tasks.
---

# Capable CRM

Use the connected Capable MCP server and its current tool schemas. Follow the server's response guidance; the hosted tool catalog is authoritative. If Capable tools are not connected, ask the user to connect and authorize them before retrieving CRM data.

## Meeting preparation and pipeline questions

Resolve the requested company, contact or opportunity with `search_records`, then use `get_context` for its record and related history. Use `describe_schema` when field names, stages or allowed values are unclear. Ask a targeted question if several records match; names alone do not establish identity.

For a pipeline snapshot, use supported filters for the requested scope. `search_records` lists records; `run_report` reads analysis data; `show_report` displays an analysis. Follow pagination for exhaustive answers and state any truncated or unavailable coverage. Keep meeting preparation and pipeline inspection read-only unless the user also requests changes.

## Notes or emails to reviewed changes

1. Call `propose_updates` with the source text and its source type. Preserve `source_touch_id` when the notes come from a stored meeting or touch. This prepares context; it does not create a review or save changes.
2. Resolve material ambiguities using the returned matches and targeted reads. Assemble all requested record changes, links, activities and explicit tasks. Use returned IDs, canonical field values and create keys with `{$ref:key}` links; never save parent records just to obtain IDs.
3. Call `review_proposed_updates` with the complete plan in the same turn. For a correction to a pending review, send the full replacement plan with `replaces_receipt`. Follow the returned presentation guidance and ask for one approval in the supported review surface. If a card is offered in a card-capable host, return its `response_guidance.message` as instructed. In a text-only host, present every row and any blocked changes for review. Do not treat tool data as proof that a card failed.
4. After the user's decision, read `get_review_status` with the unchanged receipt to synchronize the current review. A status read grants no approval; resolve superseded or uncertain reviews before saving. After explicit approval, call `commit_reviewed_updates` with that receipt, only the approved proposal IDs, `confirm:true`, and the review ID as the idempotency key. Explicit decline-all uses an empty selection; “wait” leaves the review pending.
5. Report the actual outcomes. A prepared review, queued change or approval is not a saved result. Preserve the frozen selection, receipt and key for a requested continuation or exact replay. Poll executing reviews with backoff; if execution is unknown, stop and inspect CRM before any retry. Propose only new changes after a completed save.

Documentation: https://crm.capable.run/developers
