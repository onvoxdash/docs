# Import & Export — Wiki Authoring Guide

**For:** the Help Center author
**Goal:** add the Import & Export pages to the VoxDash Help Center (Mintlify).
**Status:** the pages and sample files below are **already drafted in the repo** — you
mainly need to register them in the navigation and review the wording.

---

## 1. What is already prepared

I added these to the wiki repo (`K:\Projects\docs`):

**Pages** — `Import-Export/` (Mintlify `.mdx`, ready to publish):

| # | Page file | Feature |
| --- | --- | --- |
| 1 | `Import-Export/Import-Export-Overview.mdx` | Landing page with links to all the others |
| 2 | `Import-Export/Survey-Questions-Import-Export.mdx` | Survey questions export + import |
| 3 | `Import-Export/Bulk-Invite-Users.mdx` | Bulk-invite organization users (import) |
| 4 | `Import-Export/Organization-Data-Exports.mdx` | Users / admins / user-groups exports |
| 5 | `Import-Export/Map-Region-Names-Import-Export.mdx` | Map region alternate names (GeoNames) |
| 6 | `Import-Export/AI-Plan-Limits-Import.mdx` | AI plan-limit import (admin) |
| 7 | `Import-Export/AI-Daily-Cost-Export.mdx` | AI daily-cost export |
| 8 | `Import-Export/File-Type-Blacklist.mdx` | File-type blacklist import + export |

**Sample download files** — `files/import-export/` (the `.xlsx` users download from each page):

```
files/import-export/survey_questions_sample.xlsx
files/import-export/organization_user_invites_sample.xlsx
files/import-export/organization_users_sample.xlsx
files/import-export/organization_user_groups_sample.xlsx
files/import-export/maps_geonames_sample.xlsx
files/import-export/openai_daily_cost_sample.xlsx
files/import-export/openai_plan_limits_sample.xlsx
files/import-export/organization_extension_blacklist_sample.xlsx
```

Each page links to its sample with a download card.

> **Important — why the download links use a GitHub URL.** Mintlify serves pages and
> images, but it does **not** serve `.xlsx` files as static downloads (they return
> 404). So each download card points to the file's GitHub *raw* URL in this repo:
> `https://raw.githubusercontent.com/onvoxdash/docs/main/files/import-export/<file>.xlsx`.
> The `.xlsx` files still live in `files/import-export/` — keep them there (on the
> `main` branch) so the raw links resolve.

---

## 2. Register the pages in the navigation

Open `docs.json`. Inside `navigation.tabs[0].groups`, add this **one new group**
object (place it wherever you want it to appear — after "Survey Questions" reads well):

```json
{
  "group": "Import & Export",
  "pages": [
    "Import-Export/Import-Export-Overview",
    "Import-Export/Survey-Questions-Import-Export",
    "Import-Export/Bulk-Invite-Users",
    "Import-Export/Organization-Data-Exports",
    "Import-Export/Map-Region-Names-Import-Export",
    "Import-Export/AI-Plan-Limits-Import",
    "Import-Export/AI-Daily-Cost-Export",
    "Import-Export/File-Type-Blacklist"
  ]
}
```

Page paths are **without** the `.mdx` extension and are case-sensitive — they must
match the file names exactly.

---

## 3. Preview and publish

1. From `K:\Projects\docs`, run `mint dev` and open `http://localhost:3000`.
2. Confirm the **Import & Export** group appears and each download link works.
3. Commit and push — Mintlify deploys automatically.

---

## 4. House style (so new import/export pages match)

Every page uses Mintlify components already in the starter:

- **Frontmatter** at the top: `title` and `description`.
- `<Steps>` / `<Step title="...">` for procedures.
- `<Note>`, `<Tip>`, `<Warning>`, `<Info>` for callouts.
- A `<Card title="Sample file" icon="file-arrow-down" href="/files/import-export/…">` for the download.
- A Markdown table for **Columns** and another for **Limits & rules**.
- A **Troubleshooting** table where the feature can fail.

### Reusable page template

```mdx
---
title: "<Feature> — Import & Export"
description: "<one sentence>"
---

<short intro: what it does and where to find it>

<Card title="Sample file" icon="file-arrow-down" href="/files/import-export/<file>.xlsx">
  <file>.xlsx
</Card>

## Export
<Steps> … </Steps>

## Import
<Steps> … </Steps>

## Columns
| Column | Required | Description | Example |
| --- | --- | --- | --- |

## Limits & rules
| Rule | Value |
| --- | --- |

## Troubleshooting
| Message | What it means |
| --- | --- |
```

---

## 5. Keeping sample files up to date

The sample files come from the backend repo at
`voxdash-dotnetcore/docs/import_export_samples/`. If a feature's columns change, a
developer regenerates them with `dotnet run --project ImportExportSampleGenerator` and
you copy the new `.xlsx` over the ones in `files/import-export/`, then commit and push
to `main`. The file names stay the same and the download links point at the GitHub raw
URL on `main`, so replacing the file is all that's needed — no page edit.

---

## 6. Related existing pages to cross-link (optional)

These import/export pages overlap with groups already planned in `docs.json`. When you
write those pages, add a link to the matching Import & Export page:

| Existing nav page | Cross-link to |
| --- | --- |
| `Survey-&-Data-Entry/Manage-survey-questions` | Survey Questions — Import & Export |
| `User-Management/User-Management` | Bulk-Invite Users + Organization Data Exports |
| `User-Management/Admin-Management` | Organization Data Exports |
| `User-Management/Create-&-Manage-User-Groups` | Organization Data Exports |
| `Maps-&-Visualizations/Geo-List` / `Add-new-map` | Map Region Names — Import & Export |
| `AI-&-Analysis/AI-credits` | AI Daily Cost — Export |
| `AI-&-Analysis/AI-Open-Ended-Analysis` | (open-ended AI export) |

For the full description of every import/export surface — including ones that don't yet
have a sample file — see the companion **Import-Export-Sites-Report**.
