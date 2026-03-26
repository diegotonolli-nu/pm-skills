# pm-skills

Claude Code skills for PMs on the Shared App Experience team (Magic App BR).

## Available Skills

| Skill | Command | Description |
|---|---|---|
| pm-biweekly | `/pm-biweekly` | Generates the bi-weekly status update for senior stakeholders |
| pm-meeting | `/pm-meeting` | Transforms a meeting transcript into structured notes with context, agenda summary, decisions, and next steps |
| pm-pre-planning | `/pm-pre-planning` | Prepares the next sprint pre-planning: audits planning docs, enriches Jira descriptions, and generates an alignment .docx |
| pm-prototype | `/pm-prototype <figma-link or description>` | Generates the code for a new screen in the `br-magic-app-prototype-main` prototype |

## Installation

### Option 1 - via marketplace (recommended)

Add this repo as a marketplace in your `settings.json`:

```json
{
  "extraKnownMarketplaces": [
    {
      "name": "pm-skills",
      "url": "https://github.com/diegotonolli-nu/pm-skills"
    }
  ]
}
```

Then install:

```
/plugin marketplace add diegotonolli-nu/pm-skills
/plugin install pm-biweekly@pm-skills
/plugin install pm-meeting@pm-skills
/plugin install pm-pre-planning@pm-skills
/plugin install pm-prototype@pm-skills
```

### Option 2 - manual

Copy the files from `plugins/pm/pm-biweekly/commands/`, `plugins/pm/pm-meeting/commands/`, `plugins/pm/pm-pre-planning/commands/`, and `plugins/pm/pm-prototype/commands/` to `~/.claude/commands/`.

## Customization

Each skill was developed for the Aspirational App Spaces context, but is easily adaptable. Configure in your `CLAUDE.md` the URLs for the Program Tracker, the consolidated bi-weekly doc, and the hubs/initiatives for your area.
