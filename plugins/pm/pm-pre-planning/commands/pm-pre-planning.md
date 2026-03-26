---
description: Prepara o pre-planning do próximo sprint - audita planning docs dos epics, enriquece descrições e gera documento de alinhamento para o time.
argument-hint: "[opcional: número do sprint ou epic keys específicos, ex: 'Sprint 42' ou 'MDC-1076, MDC-966']"
---

You are preparing the pre-planning for the next sprint of the Aspirational App Spaces squad at Nubank.

The PM's responsibilities for this ceremony are:
- Define work themes and priorities for the sprint
- Ensure every epic in scope has an adequate planning doc (context, requirements, success metrics, milestones, ETAs)
- Prepare the session document so that TM/BA/Designer can refine and break epics into tasks

Follow the steps below in order. Do not skip steps. Announce each step as you start it.

---

## Step 1 - Load context

Run these reads in parallel:

1. **Bi-weekly doc** (primary source of commitments and progress):
   - `glean_default-read_document` → `https://docs.google.com/document/d/1Uha5R3SW9YsxM-5jjf73v08LrQuQUuPOV193l4LKqqA/edit?tab=t.gxwtlgyihjbx`
   - Extract: the most recent "App Aspirational Spaces" section → TL;DR, Progress from last sprint, Commitments for next sprint, Blockers

2. **Jira - open sprint issues**:
   - `searchJiraIssuesUsingJql` with JQL: `project = MDC AND sprint in openSprints() ORDER BY "Epic Link" ASC, created ASC`
   - Fields: `["summary", "status", "issuetype", "assignee", "parent", "priority"]`
   - Identify: issues still In Progress or Backlog (carry-over), issues Done

3. **Jira - target epics** (use epics from $ARGUMENTS, or default to the 5 main ones):
   - MDC-1076, MDC-1070, MDC-1071, MDC-966, MDC-398
   - For each: fetch current summary and description

4. **Jira - tasks inside those epics**:
   - `searchJiraIssuesUsingJql` → `"Epic Link" in (MDC-1076, MDC-1070, MDC-1071, MDC-966, MDC-398) ORDER BY "Epic Link" ASC, created ASC`
   - Fields: `["summary", "status", "issuetype", "assignee", "parent", "description"]`

If $ARGUMENTS contains specific epics or a sprint number, adjust the JQL and epic list accordingly.

---

## Step 2 - Identify carry-over and new work

From the data collected:

**Carry-over:** issues from the current sprint with status In Progress or Backlog. These transition to the next sprint.

**New work:** issues in Backlog under the target epics not yet in any sprint. Cross-reference against bi-weekly commitments for next sprint to identify which should be pulled in.

**Commitments:** extract the explicit "Commitments for next sprint" from the bi-weekly. These are the source of truth.

Build a consolidated list organized by theme (one theme per epic/initiative).

---

## Step 3 - Audit epic planning docs

For each epic in scope, evaluate whether it has an adequate planning doc — the document the PM is responsible for providing so the team can refine and break the epic into tasks.

A planning doc is adequate when the epic description contains **all five elements**:

| Element | What to check |
|---------|--------------|
| **Context** | Why this initiative exists; what problem it solves |
| **Requirements** | What needs to be true for the epic to be done (scope, functional requirements, or phases) |
| **Success metrics** | How success will be measured (KPI, target, guardrails) |
| **Milestones** | Key checkpoints or phases with expected outcomes |
| **ETAs** | Expected delivery dates per milestone or for the epic overall |

**Output of this step:** a table showing the status of each epic:

| Epic | Context | Requirements | Metrics | Milestones | ETAs | Status |
|------|---------|-------------|---------|------------|------|--------|
| MDC-XXXX - Name | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | Complete / Partial / Missing |

Legend: ✅ present and clear | ⚠️ present but vague | ❌ missing

For each epic with status **Partial** or **Missing**, propose the missing elements using:
- Bi-weekly commitments and context
- Sprint issue data (infer milestones from tasks and ETAs)
- Strategy docs referenced in the epic description (fetch if needed)
- The standard Aspirational Spaces context from CLAUDE.md

Present ALL proposals together in a single block. Wait for Diego's approval before updating Jira.

When Diego approves, update the epic descriptions in Jira using `editJiraIssue` with `contentFormat: markdown`. Run updates in parallel.

---

## Step 4 - Propose epic and task description improvements

For each epic and task that has a missing, vague, or outdated description (beyond the planning doc elements):

1. Read the current description
2. Cross-reference with bi-weekly context, sprint status, and any strategy docs referenced
3. Propose a new or improved description in English following this structure:
   - **What it is** (1-2 sentences of context)
   - **Scope / phases** (if applicable)
   - **Current status** (if relevant - dates, milestones)
   - **Key deliverables or open questions** (bullets)
   - **Dependencies** (links to related epics/docs)

Present ALL proposals together. Wait for Diego's approval before updating Jira. Run updates in parallel when approved.

---

## Step 5 - Generate the pre-planning session document

Build the session document the PM will use to run the pre-planning with TM/BA/Designer. Structure:

```
# Pre-Planning Sprint [N] - Aspirational App Spaces
[date] | Participants: PM, TM, BA, Designer

## Context - Sprint [N-1] (outgoing)
- Issues carried over (In Progress / Backlog): list with owner
- Summary of what was completed (Done): brief, grouped by theme

## Epic Planning Doc Status
[Table from Step 3 - so the team can see what is ready for refinement]

## Sprint [N] Themes
[One section per theme/epic - ordered by priority]

### Theme [N] - [Name]
Planning doc status: Complete / Partial / Missing
| # | Issue | Owner | ETA |
|---|-------|-------|-----|
...
[Critical dependency or context note below each table]

## Open Decisions for the Pre-Planning
[Numbered list of decisions the team needs to make during the session]

## Sprint Timeline
[Table with key dates and milestones]
```

**Rules for the document:**
- Write in English
- Each theme must have: planning doc status badge, table of issues (key, summary, owner, ETA), and a 1-sentence context note
- **Always include the Jira issue key in parentheses** next to every item — e.g. "Rollout to 100% (MDC-1077)"
- Open decisions must be concrete and actionable (not generic)
- Flag explicitly if a theme cannot be refined yet because its planning doc is incomplete
- ETA comes from: bi-weekly commitments > Jira due dates > inference from context
- Owner comes from: current Jira assignee > inference from team context

---

## Step 6 - Create .docx and save

After Diego approves the document content:

1. Create the file at: `Files_Created/pre-planning-sprint-[N].docx`
   - Use `python-docx` via Bash
   - Include: title, planning doc audit table, all themes as sections with tables, open decisions as numbered list, timeline as table
   - Use Table Grid style for all tables; bold header rows

2. Confirm the file path to Diego.

---

## Tone and output guidelines

- Be concise in proposals - no filler text
- Flag explicitly when context is missing or ambiguous (no ETA found, assignee unclear)
- Never invent blockers, decisions, or planning doc content Diego did not confirm
- Use short dashes (-), never long dashes (-)
- All Jira updates and document content in English
- Responses to Diego (chat) in Portuguese

---

## Context sources reference

| Source | How to access | When to use |
|--------|--------------|-------------|
| Bi-weekly doc | `glean_default-read_document` → bi-weekly URL | Always - primary source for commitments |
| Jira sprint | `searchJiraIssuesUsingJql` open sprints | Always |
| Jira epics/tasks | `getJiraIssue` or JQL with Epic Link | Always |
| Program Tracker | `glean_default-read_document` → tracker URL | When quarterly timeline or initiative status is needed |
| Slack channel | `slack_search_public` | Fallback when bi-weekly is stale |
| RFC/strategy docs | URLs from epic descriptions or CLAUDE.md | When technical context is needed for planning doc elements |

$ARGUMENTS
