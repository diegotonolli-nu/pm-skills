# pm-skills

Skills de Claude Code para PMs do time de Shared App Experience (Magic App BR).

## Skills disponíveis

| Skill | Comando | Descrição |
|---|---|---|
| pm-biweekly | `/pm-biweekly` | Gera o bi-weekly update de status para stakeholders sênior |
| pm-meeting | `/pm-meeting` | Transforma transcrição de reunião em ata com contexto, resumo da agenda, decisões e próximos passos |
| pm-pre-planning | `/pm-pre-planning` | Prepara o pre-planning do próximo sprint: audita planning docs, enriquece descrições no Jira e gera .docx de alinhamento |
| pm-prototype | `/pm-prototype <link-figma ou descrição>` | Gera o código de uma nova tela para o protótipo `br-magic-app-prototype-main` |

## Instalação

### Opção 1 - via marketplace (recomendado)

Adicione este repo como marketplace no seu `settings.json`:

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

Depois instale:

```
/plugin marketplace add diegotonolli-nu/pm-skills
/plugin install pm-biweekly@pm-skills
/plugin install pm-meeting@pm-skills
/plugin install pm-pre-planning@pm-skills
/plugin install pm-prototype@pm-skills
```

### Opção 2 - manual

Copie os arquivos de `plugins/pm/pm-biweekly/commands/`, `plugins/pm/pm-meeting/commands/`, `plugins/pm/pm-pre-planning/commands/` e `plugins/pm/pm-prototype/commands/` para `~/.claude/commands/`.

## Customização

Cada skill foi desenvolvida para o contexto de Aspirational App Spaces, mas é facilmente adaptável. Configure no seu `CLAUDE.md` as URLs do Program Tracker, doc consolidado de bi-weekly e os hubs/iniciativas da sua área.
