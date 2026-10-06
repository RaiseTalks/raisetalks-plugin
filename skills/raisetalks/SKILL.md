---
name: raisetalks
description: Use when the user wants to read or update their RaiseTalks data room, browse RaiseTalks startups, or manage an investor deal pipeline through the RaiseTalks MCP tools.
---

# Working with RaiseTalks

The `raisetalks` MCP server signs the user in with their RaiseTalks account. The
account's role decides which tools are available:

- **Founders** (startup accounts) can read and edit **their own** data room.
- **Investors** can browse the startup catalog, read data rooms they have access
  to, and manage their deal pipeline.

Call `get_my_profile` first if you are unsure which role you are working with.

## Founders: editing the data room

1. **Read before you write.** Fetch the section with `get_data_room_section`
   (or the whole room with `get_data_room`) before changing it.
2. **Some updates replace whole lists.** `update_team` takes the complete team,
   and the list fields of `update_market_product` (key features, traction
   metrics, customers, competitors) replace what is stored. Merge the user's
   change into the current list and send the whole list back, or existing
   entries are lost.
3. **Other updates are partial.** `update_company_identity`, `update_financials`,
   `update_media_documents`, `update_target_persona` and the single-item
   roadmap/partner/backer tools change only the fields you pass.
4. **Dropdown fields only accept listed values.** If a write is rejected with a
   list of allowed values, pick the closest one and retry. Do not invent a value.
5. **Use only facts the user gave you.** Do not make up metrics, names or numbers
   to fill a section. Leave a field empty rather than guess.
6. **Ask before deleting.** Confirm with the user before any `delete_*` tool.
7. **Editing needs a paid plan.** Reading is free. If a write returns an upgrade
   message, pass it on to the user. Do not retry.

### Files cannot be uploaded through this connector

Pitch decks and documents (company, investment, financial, technical, cap
table) have to be uploaded in the RaiseTalks web app. Call
`prepare_pitch_deck_upload` or `prepare_document_upload` and give the user the
link it returns. After a deck is uploaded, RaiseTalks reads it and fills any
empty data-room fields by itself.

Logos and photos are the exception: if the image is already at a public URL,
set that URL directly through the matching `update_*` tool.

## Investors: catalog and pipeline

- Find startups with `list_companies`, then `get_company` for the public profile.
- `get_data_room` returns only what your access level allows. A sparse result
  usually means you do not have access yet, not that the data is missing. Say so
  instead of reporting fields as empty.
- `list_pipeline` shows your dealflow by stage. Move a startup with
  `update_pipeline_stage`.
- `add_pipeline_note` **replaces** the existing notes for that startup. Read
  them first and append if the user wants to keep them.
