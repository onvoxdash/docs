---
title: "VoxDash Help-Center Coverage Gaps"
subtitle: "Pages in voxdash-public & voxdash-dataprovider with no wiki link"
date: "2026-06-20"
---

# Overview

This report lists user-facing **pages/surfaces** in the two VoxDash frontends
(`voxdash-public` and `voxdash-dataprovider`) that currently have **no help/wiki
link**, so the team can decide where to add help-center content.

A useful nuance: most of these gaps **already have a help-center article** in
the `docs` repo — the article is simply never wired into the page. So the work
splits into two kinds:

- **Wire it** — the help-center article exists; it just needs to be added to the
  page's `components/infoButton/WikiURLs.tsx` registry and rendered via an
  `InfoButton`.
- **Write new** — no article exists yet; a new `.mdx` page is needed.

# Method

A page is considered **covered** when it (or any component it renders) shows the
`?` `InfoButton` fed by `getWikiLinks(...)` or `ModalTitleWithInfo wikiKey="..."`.

Every route in both apps (`app/[locale]/**/page.tsx`) was enumerated and traced
into its `features/` / `components/` render chain, then checked against the
authoritative set of help-wired files. Pure infrastructure routes (auth, 404,
forbidden, payment/checkout, setOrgId) are excluded.

# voxdash-dataprovider — pages with no help link

| Page (route) | What it is | Help-center article? | Action |
|---|---|---|---|
| `questionnairebuilder` (+ `editor/[id]`, `import/[id]`, `quota/[id]`) | Questionnaire builder list + editor + import + quota | Yes — `Questionnaire-Builder/QB-List`, `QB-Create`, `Editorpanel-Qtype` | **Wire it** (biggest gap; docs already written) |
| `topics` | Topic approval / list | Yes — `Survey-&-Data-Entry/Topics-List` | Wire it |
| `notifications` | Notifications center | Yes — `User-Central/Notifications` | Wire it |
| `subscriptionList` | Active subscriptions list | Yes — `Billing…/subscription-management` | Wire it |
| `datasets` | Datasets / projects list | Yes — `Data-Projects/Data-Project-List` | Wire it |
| `dataProfiles` / `dataprofile/[id]` | Data-profile list + detail (`components/dataProfile/mainPage.tsx`; the data-entry form is already covered) | Yes — `Survey-&-Data-Entry/Data-Profile-Guide` | Wire it |
| `termsAndConditionsAcceptedUsers/[id]` | Accepted-users list for a T&C version | Yes — `Terms-&-Legal/View-Accepted-Terms` | Wire it |
| `termsAndConditionsVersionsHistory/[id]` | T&C version history | Yes — `Terms-&-Legal/Terms-and-Contract-History` | Wire it |
| `surveyDatasets` | Survey datasets list | No | **Write new** |
| `fieldValues` | Field-value approval interface | No | **Write new** |
| `free` / `pricing` | Free-tier / pricing marketing | Partial — `Billing…/Plans` | Optional |

# voxdash-public — pages with no help link

| Page (route) | What it is | Help-center article? | Action |
|---|---|---|---|
| `vendors` | Vendors directory (list); detail page is covered | Yes — `Vendors-&-Individuals/Vendors-Directory` | Wire it |
| `individuals` | Individuals directory (list); detail is covered | Yes — `Vendors-&-Individuals/Individuals-Directory` | Wire it |
| `datasets` | Public dataset catalog (only per-column `SortHeader`, no page-level help) | Yes — `Data-Projects/Data-Project-List` | Wire it |
| `notifications` | Standalone notifications page | Yes — `User-Central/Notifications` | Wire it |
| `advancedSearchResult` | Advanced search results | Yes — `Data-Projects/Advanced-Search` | Wire it |
| `trendManagement` | Trend management | Yes — `Data-Projects/Trend-Analysis` | Wire it |
| `profile/contactInfo` | Contact-info profile tab (other profile tabs covered) | Likely — `User-Central/User-Profile-Page` | Wire it |
| `plans` / `compare` / `free` | Plans, plan comparison, public-publishing CTA | Partial — `Billing…/Plans` | Optional |
| `surveys` | Surveys list | No | **Write new** |
| `shareyourdata` | Data-contribution CTA / form | No | **Write new** |
| `survey-preview/[token]` | Survey preview (niche) | No | Optional / write new |
| `faq`, `policies/[name]`, `page/[name]` | FAQ / legal / CMS pages | n/a | Skip (not product help) |

# Bottom line

- **Truly new wiki to write** (no article exists today): DP `surveyDatasets`,
  DP `fieldValues`, public `surveys`, public `shareyourdata`
  (+ optionally public `survey-preview`).
- **Everything else above already has a help-center article — it just isn't
  linked** in `components/infoButton/WikiURLs.tsx`.
- The single highest-value item is the **Questionnaire Builder** (full
  editor / import / quota flow), which has three docs pages already written and
  zero links.
