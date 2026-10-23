# WM8 + Portal Rollout Schedule

A single self-contained HTML page showing the partner rollout schedule for the Webmail 8 + Portal upgrade. Open `wm8_portal_rollout_schedule.html` in a browser — no build step or server needed.

The page groups HIDs into batches (retail, `custom_name` branding groups, internal infrastructure, and webmail clusters), assigns each batch a Tuesday/Thursday rollout date while skipping Canadian/Ukrainian holidays and the Dec 11 – Jan 8 code freeze, and computes the 30-day partner notice and 3/7-day team lead-time dates. The full ruleset is documented on the page itself under **Fixed constraints** and **How this sequence was built**.

## Data sources

The batch data was compiled from internal Google Sheets (linked on the page under **Data sources**):

- Branding sheet (`custom_name` groupings)
- Webmail logins / cluster workbook (30-day login counts)
- AG Report with added HID info

## Updating

Everything lives inside the one HTML file's `<script>` block:

| What | Where |
|---|---|
| Batches, HIDs, logins, deferred/suspended lists | `const DATA = {...}` |
| Rollout start date | `startStr` in `buildSchedule()` |
| Holidays and freeze weeks | `const HOLIDAYS` |
| Code freeze window | `CODE_FREEZE_START` / `CODE_FREEZE_END` |
| Batch cap (5 HIDs for the first 4 batches) | `CAP`, `CAPPED_BATCH_COUNT` |
| Cluster sizes (for the "Total HIDs in cluster" column) | `CLUSTER_TOTAL_HIDS` |

Note: some summary text in the HTML (batch/HID totals, the last-2026 and first-2027 batch dates) is written by hand and must be updated manually when the data or start date changes.

## Confidentiality

Contains internal partner names, HIDs and usage figures. Keep this repository private.
