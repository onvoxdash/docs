# VoxDash Import / Export — Sites Report

**Purpose:** a complete map of every place in VoxDash where a user downloads data
(export) or uploads a spreadsheet to make bulk changes (import), what each one does,
and which wiki page + sample file documents it.

**How to read this:** Section A lists the features that already have a drafted wiki
page and a downloadable sample file. Section B lists the remaining import/export
surfaces that still need a wiki page (no sample file yet).

---

## At a glance

| Feature | Direction | Wiki page (sample file) | Sample download |
| --- | --- | --- | --- |
| Survey questions | Export + Import | `Import-Export/Survey-Questions-Import-Export.mdx` | `survey_questions_sample.xlsx` |
| Bulk-invite users | Import | `Import-Export/Bulk-Invite-Users.mdx` | `organization_user_invites_sample.xlsx` |
| Organization users | Export | `Import-Export/Organization-Data-Exports.mdx` | `organization_users_sample.xlsx` |
| Organization admins | Export | `Import-Export/Organization-Data-Exports.mdx` | (same shape as users) |
| User groups | Export | `Import-Export/Organization-Data-Exports.mdx` | `organization_user_groups_sample.xlsx` |
| Map region names | Export + Import | `Import-Export/Map-Region-Names-Import-Export.mdx` | `maps_geonames_sample.xlsx` |
| AI plan limits | Import (admin) | `Import-Export/AI-Plan-Limits-Import.mdx` | `openai_plan_limits_sample.xlsx` |
| AI daily cost | Export | `Import-Export/AI-Daily-Cost-Export.mdx` | `openai_daily_cost_sample.xlsx` |
| File-type blacklist | Export + Import | `Import-Export/File-Type-Blacklist.mdx` | `organization_extension_blacklist_sample.xlsx` |

All sample files live in `files/import-export/` in this wiki repo.

---

## Section A — Documented features (page + sample ready)

### A1. Survey questions
- **Where:** Data Provider → Survey → Questions tab.
- **What:** export questions + answer options to Excel; edit the text; re-import to bulk-update.
- **Columns:** Variable Name, Question Title, Response ID, Response Title.
- **Key rules:** `.xlsx` only, max 10 MB; matched by header name; needs survey edit access.
- **Wiki page:** `Import-Export/Survey-Questions-Import-Export.mdx` · **Sample:** `survey_questions_sample.xlsx`.

### A2. Bulk-invite users
- **Where:** Data Provider → Organization → User management.
- **What:** upload a spreadsheet of people, preview the rows, and invite the selected ones.
- **Columns:** Salutation, First name, Last name, Email.
- **Key rules:** `.xlsx` only, max 10 MB; email must be unique; flexible name headers.
- **Wiki page:** `Import-Export/Bulk-Invite-Users.mdx` · **Sample:** `organization_user_invites_sample.xlsx`.

### A3. Organization users / admins / user groups (export-only)
- **Where:** Organization → User management / Admin management / User groups.
- **What:** download the current list to Excel for reporting.
- **Columns:** users/admins — Salutation, First Name, Last Name, Email, Access Type, Date Added; groups — Name, Description, Member Count, Date Created.
- **Wiki page:** `Import-Export/Organization-Data-Exports.mdx` · **Samples:** `organization_users_sample.xlsx`, `organization_user_groups_sample.xlsx`.

### A4. Map region names (GeoNames)
- **Where:** Data Provider → Maps.
- **What:** export a map's regions; add alternate names in the "Add Alternate Names" column; re-import to attach them.
- **Columns:** GeoNameId, Region Name, Existing Alternate Names, Add Alternate Names.
- **Key rules:** `.xlsx` only, max 10 MB, max 50,000 rows, 50 new names/row, 200 names/region; names separated by `|`, `;`, or new line.
- **Wiki page:** `Import-Export/Map-Region-Names-Import-Export.mdx` · **Sample:** `maps_geonames_sample.xlsx`.

### A5. AI plan limits (admin import)
- **Where:** Administrator → AI plan limits.
- **What:** bulk-set default/maximum token limits per plan, task type, and model.
- **Columns:** PlanId, TaskType, ModelId, IsDefaultModel, DefaultInputToken, DefaultOutputToken, MaxInputToken, MaxOutputToken.
- **Key rules:** `.xlsx` only, max 5 MB, max 5,000 rows; unique (PlanId, TaskType, ModelId); one default model per (PlanId, TaskType).
- **Wiki page:** `Import-Export/AI-Plan-Limits-Import.mdx` · **Sample:** `openai_plan_limits_sample.xlsx`.

### A6. AI daily cost (export-only)
- **Where:** Data Provider → AI Credits.
- **What:** export a day-by-day AI cost breakdown.
- **Columns:** Date, Input Cost, Output Cost, File Cost, Total Cost.
- **Wiki page:** `Import-Export/AI-Daily-Cost-Export.mdx` · **Sample:** `openai_daily_cost_sample.xlsx`.

### A7. File-type blacklist
- **Where:** Organization → file-type settings.
- **What:** export the current blocked-extension list; import a replacement list.
- **Columns:** Extensions (one per row).
- **Key rules:** `.xlsx` only, max 2 MB, max 2,000 extensions; replaces the whole list; an empty result is rejected so it can't wipe the list.
- **Wiki page:** `Import-Export/File-Type-Blacklist.mdx` · **Sample:** `organization_extension_blacklist_sample.xlsx`.

---

## Section B — Other import/export surfaces (page still needed, no sample file)

These exist in the product but don't have a structured-spreadsheet sample. Document
them on the related existing nav page (suggested below) when you reach it.

| Surface | Direction | Format | Where in app | Suggested wiki home |
| --- | --- | --- | --- | --- |
| Questionnaire import from document | Import | .doc/.docx/.xls/.xlsx/.pdf/.sav/.sps | Questionnaire Builder → Import | Questionnaire-Builder group |
| Quota configuration | Export + Import | .xlsx / .json | Questionnaire Builder → Quota | Questionnaire-Builder group (the app provides its own in-product sample) |
| Contract / Terms version file | Import | PDF / Word / XLSX | Organization → Contract settings | Terms-&-Legal group |
| Terms & Conditions / Contract document | Export | PDF | Public dataset → Overview | Terms-&-Legal group |
| Dataset files | Export | any (xlsx, csv, pdf, zip, image…) | Public dataset → Files tab | Data-Management group |
| Question / Trend results | Export | XLSX | Public question / trend page | Survey-Questions group |
| Crosstab / Regional results | Export | XLSX / PDF | Public crosstab page | Reports-&-Dashboards group |
| Activity / chart reports | Export | XLSX | Data Provider → Reports | Reports-&-Dashboards group |
| Generic file upload | Import | any | File manager / dataset editor (Uppy) | Data-Management → Bulk-File-Upload |

<!-- Internal only, not user-facing: breached-password list upload (admin .txt). Omit from the Help Center. -->

---

## Notes

- **Round-trip principle:** for the spreadsheet features in Section A, the export file
  *is* the import template — export first, edit, re-upload. The sample files were
  generated through the same export code the product uses, so their headers match the
  importers exactly.
- **Filename pattern:** backend-generated exports are named
  `{feature}_{entity}_{yyyyMMdd_HHmmss}.xlsx`.
- **Source of samples:** `voxdash-dotnetcore/docs/import_export_samples/` (regenerate with
  `dotnet run --project ImportExportSampleGenerator`). The companion **Authoring Guide**
  explains how to refresh them.
