# AI contracts ledger

Publicly announced AI data-center capacity deals, in gigawatts, one row per
announcement, each with a source link and a short quotation containing the
capacity figure. This file is the **master copy** read by the "AI Build-out" tab
of Market Big Picture and Long-term Strategies (`ai_ledger_url` in its
config.ini points at this repo's raw `ai_contracts.csv`). Reviewed weekly.

Method and caveats, in full: the dashboard's `/methodology` page.

## Columns

| column | meaning |
|---|---|
| `id` | unique, stable: `<date>-<group>` (add `-2` on a clash). Never change an existing id. |
| `date` | announcement date, `YYYY-MM-DD` (month-only: use the 1st and say so in `notes`) |
| `end_date` | blank, or the date the deal was cancelled / lapsed -- it stops counting that day |
| `buyer` | the capacity user / offtaker |
| `counterparty` | supplier, landlord, developer or utility |
| `gw` | capacity in GW as stated by the source (MW / 1000). **Never inferred** from dollars, GPUs or floor area. Minimum 0.3. |
| `type` | `cloud` (compute-capacity contract) · `lease` (colocation / campus lease) · `chips` (accelerator deployment in GW) · `power` (PPA / dedicated generation) · `site` (announced campus, mostly self-build) |
| `binding` | `definitive` (source says signed / definitive agreement / lease executed) · `loi` (LOI, MOU, term sheet, "strategic partnership") · `plan` (unilateral build announcement) · `unknown` |
| `group` | rows describing the SAME physical gigawatts share a group; the dashboard counts a group once, at its largest `gw`. A new, separate deal gets a new group. |
| `count` | `1`, or `0` = listed but not summed (goals, umbrella totals whose parts are listed, supplier partnerships with no end user, campuses with no tenant). Say why in `notes`, starting `NOT COUNTED:`. |
| `status` | `ok` (verified against the source) · `review` (unverified proposal, never counted) · `reject` |
| `location` | if stated |
| `source_url` | `https://` link to the page that states the figure. Prefer the press release / SEC filing. |
| `quote` | <= 25 words copied from the source, containing the capacity figure |
| `notes` | caveats: later resized, basis (critical IT vs gross), overlaps with other rows, secondary sources |

## Rules for editing

1. A row is added only after opening its source and seeing the MW/GW figure there.
2. The four layers (cloud+lease, chips, power, site) are never summed with each
   other, so the same gigawatts MAY appear once per layer. Within a layer they
   must not appear twice: reuse the existing `group` for an upsized or
   re-announced deal.
3. A cancelled or lapsed deal is not deleted: set `end_date` and explain in `notes`.
4. Keep rows sorted by `date`, then `id`. Keep the header and column order exactly.
