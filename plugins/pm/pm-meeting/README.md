# pm-meeting

Transforma a transcrição de uma reunião em ata estruturada com decisões, próximos passos e action items.

## Como usar

```
/pm-meeting
/pm-meeting https://docs.google.com/document/d/...
```

Aceita link de Google Doc ou transcrição colada diretamente no chat.

## O que o agente faz

1. Identifica automaticamente o tipo de reunião (alinhamento, design review, 1:1, incidente, etc.)
2. Extrai participantes, decisões, próximos passos e perguntas em aberto
3. Destaca compromissos assumidos pelo PM
4. Sugere onde documentar cada item (Confluence, Jira, etc.)
