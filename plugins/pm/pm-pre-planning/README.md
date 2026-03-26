# pm-pre-planning

Prepara o pre-planning do próximo sprint do squad de Aspirational App Spaces em 6 passos estruturados.

## Como usar

```
/pm-pre-planning
/pm-pre-planning Sprint 42
/pm-pre-planning MDC-1076, MDC-966
```

## O que o agente faz

1. **Carrega contexto** - lê o bi-weekly doc e o Jira (sprint aberto + epics-alvo) em paralelo
2. **Identifica carry-over e novo trabalho** - cruza issues do sprint com commitments do bi-weekly
3. **Audita planning docs dos epics** - avalia se cada epic tem contexto, requirements, métricas, milestones e ETAs; propõe os elementos faltantes
4. **Enriquece descrições** - propõe melhorias nas descrições de epics e tasks; atualiza no Jira após aprovação
5. **Gera documento de sessão** - cria o doc de pre-planning com temas, tabelas de issues, decisões em aberto e timeline
6. **Exporta .docx** - salva em `Files_Created/pre-planning-sprint-[N].docx`

## Epics-alvo padrão

MDC-1076, MDC-1070, MDC-1071, MDC-966, MDC-398

Substitua passando epic keys como argumento.

## Customização

Configure no seu `CLAUDE.md`:
- URL do doc consolidado de bi-weekly do time
- URL do Program Tracker da sua área
- Epic keys padrão para o pré-planning
- Contexto do time (nomes/papéis dos membros para atribuição de owners)
