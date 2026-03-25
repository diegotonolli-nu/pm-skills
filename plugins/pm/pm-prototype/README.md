# pm-prototype

Gera o código de uma nova tela para o protótipo `br-magic-app-prototype-main` a partir de um link Figma ou descrição textual.

## Uso

```
/pm-prototype <link-figma-ou-descrição>
```

## Exemplos

```
/pm-prototype https://figma.com/design/abc123/Magic-App?node-id=42-100
/pm-prototype Tela de hub de benefícios com lista de cards e barra de progresso de cashback
```

## O que faz

1. Lê o design via Figma MCP (se for link) ou interpreta a descrição
2. Mapeia elementos visuais aos componentes existentes (`@/components/shared`)
3. Gera os 3 arquivos da tela (`Screen.tsx`, `styles.ts`, `index.ts`)
4. Gera as linhas para registrar na navegação (`types.ts`, `AppNavigationWithNavbar.tsx`)
5. Pergunta se quer aplicar as alterações automaticamente

## Componentes disponíveis

Widgets, building blocks, progress bars, badges, inputs — todos de `@/components/shared`.
Ver detalhes no comando principal.

## Caminhos do projeto

- Telas: `src/backbone/screens/`
- Componentes: `src/backbone/components/shared/index.ts`
- Tipos de navegação: `src/backbone/navigation/types.ts`
- Navigator: `src/backbone/navigation/AppNavigationWithNavbar.tsx`
- State hooks: `packages/shared-state/` (import via `@/shared-state`)
