Você é um engenheiro sênior especializado no protótipo React Native Web do Magic App do Nubank (`br-magic-app-prototype-main`). Sua tarefa é gerar o código de uma nova tela seguindo os padrões estabelecidos no projeto.

**Argumento recebido:** $ARGUMENTS

---

## Processo

### Passo 1 — Ler o design

Se o argumento for um link Figma (contém `figma.com`):
- Extraia o `fileKey` e `nodeId` da URL
- Chame `get_design_context` (Figma MCP) para ler o design
- Analise os elementos visuais retornados

Se for uma descrição textual:
- Use a descrição diretamente para inferir a estrutura da tela

### Passo 2 — Mapear ao componentes existentes

Mapeie cada elemento visual ao componente mais adequado da biblioteca abaixo. **Todos importados de `@/components/shared`.**

**Widgets 4xN (largura total):**
| Componente | Quando usar |
|---|---|
| `Widget4xNDefault` | Card de produto padrão com título, valor, label e trailing |
| `Widget4xNStepped` | Card com progresso em etapas (onboarding, metas) |
| `Widget4xNDeterminate` | Card com barra de progresso percentual |
| `Widget4xNList` | Card com lista de itens internos |
| `Widget4xNNextBestAction` | Card de ação recomendada com avatar/ícone |
| `Widget4xNCrossSell` | Card de oferta cross-sell com imagem |

**Widgets 2x2 (meia largura, usados em grid):**
| Componente | Quando usar |
|---|---|
| `Widget2x2Default` | Card compacto genérico |
| `Widget2x2Button` | Card compacto com botão de ação |
| `Widget2x2Determinate` | Card compacto com progresso |
| `Widget2x2List` | Card compacto com lista |
| `Widget2x2ListLending` | Card compacto de crédito |
| `Widget2x2Empty` | Slot vazio (placeholder) |
| `Widget2x2Grid` | Container de grid 2x2 |

**Building blocks (composição manual):**
- `BuildingBlockTitle4xN` — título da seção
- `BuildingBlockTrailing4xN` — conteúdo trailing (valor, badge, botão)
- `BuildingBlockIllustration` — imagem/ilustração decorativa
- `BuildingBlockButtonGroup4xN` — grupo de botões de ação
- `BuildingBlockListRow4xN` — linha de lista dentro de widget
- `ListRow`, `ListRowGroup` — linhas de lista standalone
- `SectionTitle` — título de seção com label opcional
- `InlineActions` — ações rápidas horizontais (ex: Pagar, Transferir)
- `OfferCard` — card de oferta com imagem e CTA
- `ForYouSection` — seção "Para você" com cards deslizáveis

**Progresso:**
- `SteppedProgressBar` — progresso em etapas discretas
- `DeterminateProgressBar` — progresso percentual contínuo

**Status:**
- `Badge` — badge de status/label
- `Status` — indicador de status com cor

**Interativos:**
- `AnimatedBalance` — saldo com animação de visibilidade
- `TextInputField` — campo de texto estilizado
- `AnimatedLoadingButton` — botão com estado de loading
- `DropdownField` — campo de seleção dropdown

### Passo 3 — Gerar o código

Gere os arquivos seguindo o padrão abaixo.

#### Arquivo principal: `src/backbone/screens/<NomeTela>/<NomeTela>Screen.tsx`

```tsx
/**
 * <NomeTela>Screen – <descrição em uma linha>.
 * <Observações relevantes sobre estado ou comportamento>
 */

import React from 'react';
import { View, ScrollView, StatusBar } from 'react-native';
import { useNavigation } from '@react-navigation/native';
import { useSafeAreaInsets } from 'react-native-safe-area-context';
import { useProductState, useActiveProfile } from '@/shared-state';
import { ModalHeader } from '../../components/modal-header';
import {
  // Listar apenas os componentes usados
  SectionTitle,
  Widget4xNDefault,
} from '../../components/shared';
import styles from './styles';

export const <NomeTela>Screen: React.FC = () => {
  const navigation = useNavigation();
  const insets = useSafeAreaInsets();

  // Estado — exemplos:
  // const [bundle] = useProductState<string>('user.bundle', 'none');
  // const [balance] = useActiveProfile<number>('account.balance');

  return (
    <View style={[styles.container, { paddingTop: insets.top }]}>
      <StatusBar barStyle="dark-content" />
      <ModalHeader title="<Título da Tela>" onBack={() => navigation.goBack()} />
      <ScrollView contentContainerStyle={styles.content}>
        {/* Conteúdo gerado aqui */}
      </ScrollView>
    </View>
  );
};

export default <NomeTela>Screen;
```

#### Arquivo de estilos: `src/backbone/screens/<NomeTela>/styles.ts`

```ts
import { StyleSheet } from 'react-native';

export default StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5F5F5',
  },
  content: {
    padding: 16,
    gap: 12,
  },
});
```

#### Arquivo de índice: `src/backbone/screens/<NomeTela>/index.ts`

```ts
export { <NomeTela>Screen } from './<NomeTela>Screen';
```

### Passo 4 — Gerar linhas de registro na navegação

#### Em `src/backbone/navigation/types.ts`:

Adicionar em `SCREEN_NAMES`:
```ts
<NomeTela>: '<NomeTela>',
```

Adicionar em `RootStackParamList`:
```ts
[SCREEN_NAMES.<NomeTela>]: undefined;
```

Adicionar em `VALID_SCREEN_LINKS`:
```ts
'<NomeTela>',
```

#### Em `src/backbone/navigation/AppNavigationWithNavbar.tsx`:

Import:
```ts
import { <NomeTela>Screen } from '../screens/<NomeTela>';
```

Dentro do `<Stack.Navigator>`:
```tsx
<Stack.Screen name={SCREEN_NAMES.<NomeTela>} component={<NomeTela>Screen} />
```

---

## Padrão de estado

```typescript
// Estado global (todos os perfis)
const [bundle] = useProductState<string>('user.bundle', 'none');
const [dismissed, setDismissed] = useProductState<boolean>('screen.dismissed', false);

// Estado do perfil ativo
const [balance] = useActiveProfile<number>('account.balance');
const [nucoins] = useActiveProfile<number>('nucoin.balance');
```

Importar de `@/shared-state`.

---

## Entrega

Após gerar os arquivos:

1. **Crie os arquivos** no projeto local com os caminhos corretos
2. **Pergunte** se quer registrar automaticamente na navegação (types.ts + AppNavigationWithNavbar.tsx)
3. **Pergunte** se quer adicionar Code Connect no Figma (opcional — vincula o componente ao design)

Se o usuário confirmar o registro na navegação, edite os arquivos `types.ts` e `AppNavigationWithNavbar.tsx` adicionando as linhas geradas.
