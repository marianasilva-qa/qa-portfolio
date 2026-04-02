# 🔍 Exploratory Testing Findings — KaBuM!

Registro de achados de uma sessão de teste exploratório conduzida no site [KaBuM!](https://www.kabum.com.br).

---

## 📋 Charter da Sessão

| Campo | Detalhe |
|---|---|
| **Área** | Fluxo de busca, filtros e carrinho |
| **Missão** | Explorar comportamentos inesperados na busca de produtos, aplicação de filtros e gestão do carrinho de compras |
| **Duração** | 30 minutos |
| **Ambiente** | Navegador Chrome 123 · Desktop · Sem conta logada |
| **Data** | 26/03/2026 |
| **Tester** | Renato Paes |
| **Hipóteses iniciais** | O total do carrinho pode não atualizar corretamente ao alterar quantidade; filtros combinados podem retornar resultados inconsistentes |

---

## 🧭 Heurísticas Utilizadas

- **CRUD** — testar criação, leitura, atualização e remoção de itens no carrinho
- **Vazio / Cheio / Limite** — testar campos e listas em estados extremos
- **Fluxo Interrompido** — testar o que acontece ao voltar, recarregar e trocar de aba

---

## 📝 Observações

### OBS-001 · Busca com campo vazio

| | |
|---|---|
| **Área** | Busca |
| **Heurística** | Vazio / Cheio / Limite |
| **Ação realizada** | Clicar no botão de busca sem digitar nada no campo |
| **Resultado esperado** | Mensagem de erro ou nenhuma ação |
| **Resultado obtido** | A página recarrega exibindo todos os produtos disponíveis, sem nenhuma mensagem ao usuário |
| **Classificação** | 🟡 Comportamento estranho — pode ser decisão de design, mas não comunica nada ao usuário |
| **Evidência** | `busca-vazia-resultado.png` |

---

### OBS-002 · Ordenação por menor preço não ordena corretamente

| | |
|---|---|
| **Área** | Listagem de produtos |
| **Heurística** | CRUD (Ler) |
| **Ação realizada** | Buscar "notebook", aplicar ordenação "Menor Preço" |
| **Resultado esperado** | Produtos listados em ordem crescente de preço |
| **Resultado obtido** | Os primeiros 3 resultados aparecem fora de ordem — produto de R$ 3.499 aparece antes de produto de R$ 2.799 |
| **Classificação** | 🔴 Bug — comportamento definitivamente diferente do esperado |
| **Evidência** | `ordenacao-menor-preco.png` |

---

### OBS-003 · Filtro de marca não atualiza contador de resultados

| | |
|---|---|
| **Área** | Filtros |
| **Heurística** | CRUD (Atualizar) |
| **Ação realizada** | Buscar "teclado", aplicar filtro por marca "Redragon" |
| **Resultado esperado** | Contador de resultados atualiza para refletir apenas os produtos da marca selecionada |
| **Resultado obtido** | O número de resultados exibido no cabeçalho ("X produtos encontrados") permanece igual ao da busca sem filtro |
| **Classificação** | 🔴 Bug — informação inconsistente com o conteúdo exibido |
| **Evidência** | `filtro-marca-contador.png` |

---

### OBS-004 · Carrinho persiste após recarregar a página

| | |
|---|---|
| **Área** | Carrinho |
| **Heurística** | Fluxo Interrompido (Recarregar) |
| **Ação realizada** | Adicionar 2 produtos ao carrinho, pressionar F5 |
| **Resultado esperado** | Comportamento indefinido — pode ou não persistir |
| **Resultado obtido** | Os produtos permanecem no carrinho após o recarregamento, sem necessidade de login |
| **Classificação** | ✅ Funciona como esperado — comportamento positivo, melhora a experiência do usuário |
| **Evidência** | — |

---

### OBS-005 · Quantidade 0 no carrinho não remove o item

| | |
|---|---|
| **Área** | Carrinho |
| **Heurística** | Vazio / Cheio / Limite · CRUD (Atualizar) |
| **Ação realizada** | Alterar manualmente a quantidade de um item no carrinho para `0` e confirmar |
| **Resultado esperado** | Item removido do carrinho, ou mensagem informando que quantidade mínima é 1 |
| **Resultado obtido** | O campo volta automaticamente para `1` sem exibir nenhuma mensagem ao usuário |
| **Classificação** | 🟡 Comportamento estranho — funciona, mas não comunica o motivo da correção |
| **Evidência** | `quantidade-zero-carrinho.png` |

---

### OBS-006 · Botão "Comprar" permanece ativo com carrinho vazio

| | |
|---|---|
| **Área** | Carrinho |
| **Heurística** | Vazio / Cheio / Limite |
| **Ação realizada** | Remover todos os itens do carrinho, observar estado do botão |
| **Resultado esperado** | Botão "Fechar Pedido" desabilitado ou removido da tela |
| **Resultado obtido** | O botão continua visível e clicável; ao clicar, redireciona para a tela de login |
| **Classificação** | 🟡 Sugestão de melhoria (UX) — funciona, mas o redirecionamento sem contexto pode confundir o usuário |
| **Evidência** | `botao-comprar-carrinho-vazio.png` |

---

### OBS-007 · Voltar do checkout mantém carrinho intacto

| | |
|---|---|
| **Área** | Checkout |
| **Heurística** | Fluxo Interrompido (Voltar) |
| **Ação realizada** | Adicionar produtos, avançar para o checkout, clicar em voltar no navegador |
| **Resultado esperado** | Carrinho mantido com os itens adicionados |
| **Resultado obtido** | Carrinho permanece com todos os itens; estado preservado corretamente |
| **Classificação** | ✅ Funciona como esperado |
| **Evidência** | — |

---

### OBS-008 · Busca com caracteres especiais retorna erro 500

| | |
|---|---|
| **Área** | Busca |
| **Heurística** | Vazio / Cheio / Limite |
| **Ação realizada** | Digitar `<script>` no campo de busca e submeter |
| **Resultado esperado** | Mensagem de "nenhum resultado encontrado" ou sanitização silenciosa da entrada |
| **Resultado obtido** | Página retorna erro HTTP 500 (Internal Server Error) |
| **Classificação** | 🔴 Bug — potencial vulnerabilidade de segurança; erro de servidor não deve ser exposto ao usuário |
| **Evidência** | `busca-caractere-especial-500.png` |

---

## 📊 Resumo dos Achados

| Classificação | Quantidade |
|---|---|
| 🔴 Bug | 3 |
| 🟡 Comportamento estranho / Sugestão de melhoria | 3 |
| ✅ Funciona como esperado | 2 |
| **Total de observações** | **8** |

---

## 🔎 Próximos Passos

- [ ] OBS-002 e OBS-003 têm potencial para virar **bug reports formais** (próximo artefato do portfólio)
- [ ] OBS-008 deve ser reportado com prioridade alta dado o impacto de segurança
- [ ] Abrir nova sessão focada no fluxo de login e criação de conta

---

## 🛠 Técnicas Aplicadas

- Teste exploratório com charter estruturado
- Heurísticas: CRUD · Vazio/Cheio/Limite · Fluxo Interrompido

---

*Sessão conduzida como parte do programa Squad Academy — QA Mentorship 2026.*
