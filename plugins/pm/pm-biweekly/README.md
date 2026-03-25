# pm-biweekly

Gera o bi-weekly update de status para stakeholders sênior no formato do time de Shared App Experience.

## Como usar

```
/pm-biweekly
/pm-biweekly Mar 13 - Mar 26
```

## O que o agente faz

1. Lê o update anterior para extrair os Commitments do sprint passado
2. Consulta o Program Tracker, Jira e Slack para coletar o status do período
3. Gera o update no formato padrão: TL;DR, Progress, Commitments e Blockers

## Customização

Antes de usar, configure no seu CLAUDE.md:
- URL do doc consolidado de bi-weekly do time
- URL do Program Tracker da sua área
- Nome da área / hubs que você gerencia
