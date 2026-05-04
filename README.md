# Documentação — Sistema PDV de Refeições

**Ponto de venda para eventos esportivos**

| Campo | Valor |
| ----- | ----- |
| Versão | 1.0 |
| Status | Rascunho |
| Data | 04/04/2026 |
| Destinatário | Equipe de desenvolvimento |
| Contexto | Evento esportivo — gestão de refeições |

---

## 1. Visão geral do produto

### 1.1 Objetivo

Este documento descreve os requisitos funcionais e não funcionais de um sistema de ponto de venda (PDV) voltado para a gestão de refeições em eventos esportivos. O sistema visa facilitar o controle de pedidos, o vínculo entre atletas e seus responsáveis, e o fechamento de contas de forma eficiente e rastreável.

### 1.2 Escopo

O sistema cobrirá os seguintes módulos:

- Configuração de tipos de refeição e itens de venda
- Gestão de clientes (atletas, pais e outros)
- Registro de pedidos por tipo de refeição
- Vinculação automática entre atleta e responsável
- Fechamento de conta com envio de comprovante por e-mail
- Relatórios de vendas (contas pagas e em aberto)
- Reset do sistema ao fechar o caixa

### 1.3 Público-alvo do sistema

Operadores do caixa durante eventos esportivos que necessitam registrar pedidos de refeições de atletas (crianças e jovens) e seus pais ou responsáveis.

---

## 2. Categorias de usuários e precificação

O sistema deve suportar diferentes categorias de usuários com regras de precificação específicas por faixa etária e por **modalidade** (**softball** ou **baseball**). Os preços de cada combinação modalidade + categoria são cadastrados previamente pelo administrador.

### 2.1 Categorias de atletas

Os atletas são classificados por **modalidade** (**softball** ou **baseball**) e por **categoria esportiva**, cada uma com faixa etária definida abaixo. O sistema deve permitir cadastrar **preços por modalidade + categoria** (e o vínculo pai/responsável segue a categoria do atleta). Em todas as linhas, salvo exceção indicada, a regra de pagamento é **valor próprio da categoria**, pré-cadastrado pelo administrador.

#### Softball

| Categoria | Faixa etária | Observação |
| --------- | ------------ | ---------- |
| TBol | Até 9 anos | Abaixo de 5 anos: isento (sem lançamento de refeição de atleta nesta categoria) |
| Sub 11 | Até 11 anos | — |
| Sub 13 | Até 13 anos | — |
| Sub 16 | Até 16 anos | — |
| Sub 19 | 17 a 19 anos | — |
| Sub 23 | 20 a 23 anos | — |
| Adulto | Acima de 23 anos | — |

#### Baseball

| Categoria | Faixa etária | Observação |
| --------- | ------------ | ---------- |
| TBol | 5 a 8 anos | Abaixo de 5 anos: isento (sem lançamento de refeição de atleta nesta faixa) |
| Pré-infantil | 9 a 10 anos | — |
| Infantil | 11 a 12 anos | — |
| Pré-júnior | 13 a 14 anos | — |
| Júnior | 15 a 16 anos | — |
| Juvenil | 17 a 18 anos | — |
| Sub 23 | 19 a 23 anos | — |
| Adulto | Acima de 23 anos | — |

### 2.2 Pais e responsáveis

Cada categoria de atleta possui um valor correspondente para os pais/responsáveis, também configurado previamente no sistema. O pai é vinculado ao atleta no cadastro, permitindo visualização cruzada dos pedidos.

### 2.3 Outras categorias

- **Parentes e amigos:** pagam valor de “refeição avulsa”.
- **Isento:** crianças abaixo de 5 anos não geram lançamento de refeição.

> Detalhamento e demais regras consolidadas: **[REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md)**.

---

## 3. Módulo: tela inicial e configuração

### 3.1 Tela inicial — tipos de refeição

Ao iniciar o sistema (ou após o fechamento do caixa), a tela inicial deve ser exibida com as opções de tipos de refeição disponíveis:

| Tipo de refeição | Descrição |
| ---------------- | --------- |
| Café da manhã | Refeições e itens do turno matutino |
| Almoço | Refeições e itens do almoço |
| Jantar | Refeições e itens do jantar |
| Barraca de vendas | Itens avulsos vendidos na barraca |
| Cadastrar diversos | Configuração de itens customizados |

### 3.2 Funcionalidade: cadastrar diversos

Esta funcionalidade permite ao operador cadastrar previamente itens que serão vendidos nos tipos de refeição. O fluxo é:

1. O usuário acessa “Cadastrar diversos” na tela inicial.
2. Informa o nome do item e o valor unitário.
3. Seleciona um ou mais tipos de refeição nos quais o item estará disponível (múltipla seleção, inclusive todos os tipos).
4. Confirma o cadastro. O item passa a aparecer nas opções de pedido do(s) tipo(s) escolhido(s).

As regras de negócio deste fluxo estão em **[REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md)** (cadastro “Diversos” e sessão).

### 3.3 Reinicialização ao fechar o caixa

Ao executar o fechamento do caixa, o sistema deve:

- Limpar todos os pedidos e consumos registrados na sessão.
- Remover os itens cadastrados em “Diversos” para a sessão atual.
- Retornar à tela inicial com os tipos de refeição disponíveis.
- Manter o cadastro permanente de clientes (atletas e pais) intacto.

---

## 4. Módulo: lista de clientes e pedidos

### 4.1 Exibição da lista de clientes

Após selecionar um tipo de refeição, o sistema exibe a lista de clientes cadastrados. Cada entrada deve mostrar:

- Nome completo
- Categoria (ex.: atleta softball Sub 13, atleta baseball infantil, pai da mesma modalidade/categoria de referência, parente, etc.)
- Idade

### 4.2 Fluxo de registro de pedido

1. O operador clica no nome do cliente desejado.
2. O sistema exibe os itens disponíveis para o tipo de refeição selecionado.
3. O operador seleciona os itens e quantidades.
4. O sistema exibe o resumo do pedido (itens + valores + subtotal).
5. O operador confirma ou cancela o pedido.
6. Somente após confirmação ou cancelamento é possível selecionar outro cliente.

### 4.3 Itens disponíveis por tipo de refeição

Exemplo de itens para o tipo **almoço**:

| Item | Disponível para | Observação |
| ---- | ---------------- | ---------- |
| Refeição (atleta/pais) | Atletas e pais | Valor pré-cadastrado por categoria |
| Refeição avulsa | Parentes e amigos | Valor pré-cadastrado |
| Refrigerante | Todos | Valor fixo |
| Cerveja | Adultos | Valor fixo |
| Água | Todos | Valor fixo |
| Diversos | Todos | Valor e descrição configurados no ato |

### 4.4 Item “Diversos” no pedido

Ao selecionar o item “Diversos” durante um pedido, o operador deve:

- Informar o nome/descrição do item no momento do pedido.
- Informar o valor unitário no momento do pedido.

O item é registrado apenas para aquele pedido específico, sem impacto no cadastro geral.

### 4.5 Resumo do pedido em tempo real

Durante a seleção de itens, o sistema deve exibir continuamente:

- Lista dos itens selecionados com quantidade e valor unitário.
- Subtotal atualizado automaticamente a cada seleção.
- Botões de confirmar e cancelar claramente visíveis.

---

## 5. Módulo: vinculação atleta–pai

### 5.1 Relacionamento entre atleta e pai

Cada atleta pode ter um pai/responsável vinculado. Esta relação deve ser cadastrada previamente. A vinculação permite:

- Ao clicar no atleta, visualizar o histórico de consumo do atleta e do pai vinculado.
- Ao clicar no pai, visualizar o histórico de consumo do pai e do atleta vinculado.
- Fechar a conta de ambos a partir de qualquer um dos dois.

### 5.2 Visualização cruzada de consumo

Exemplo prático:

1. O atleta João faz um pedido de almoço e confirma.
2. Em seguida, o operador clica no pai de João — Carlos.
3. Na tela de Carlos, além dos botões de seleção de itens, aparece o resumo do consumo de João.
4. Carlos faz seu pedido. Ao confirmar, o resumo exibe o consumo de ambos.
5. O mesmo ocorre ao clicar em João: o resumo mostra o consumo de João e de Carlos.

### 5.3 Resumo consolidado para fechamento

Ao iniciar o processo de fechamento de conta (a partir do atleta ou do pai), o sistema exibe:

- Nome do atleta e nome do pai/responsável.
- Lista de todos os itens consumidos por ambos, agrupados por tipo de refeição.
- Valor individual de cada item e quantidade.
- Total geral (atleta + pai).
- Forma de pagamento: PIX (única opção na versão inicial).
- Botão para confirmar o pagamento.

---

## 6. Módulo: fechamento de conta

### 6.1 Fluxo de fechamento

1. O operador seleciona o cliente (atleta ou pai) na lista.
2. Acessa a opção “Fechar conta”.
3. O sistema exibe o resumo consolidado (atleta + pai).
4. O operador confirma o recebimento via PIX pressionando o botão de confirmação.
5. O sistema registra a conta como paga.
6. O comprovante é enviado automaticamente por e-mail para o pai/responsável.

### 6.2 Comprovante por e-mail

O e-mail enviado ao pai deve conter:

- Nome do atleta e do pai.
- Data e hora do fechamento.
- Lista detalhada dos itens consumidos (por pessoa e tipo de refeição).
- Valor total pago.
- Identificação do evento.

### 6.3 Status das contas

| Status | Descrição | Ação disponível |
| ------ | --------- | ----------------- |
| Em aberto | Pedidos realizados, conta não paga | Adicionar itens, fechar conta |
| Paga | Pagamento confirmado pelo operador | Visualizar comprovante |
| Sem consumo | Cliente sem pedidos na sessão | Iniciar pedido |

---

## 7. Módulo: relatórios

Ao final da sessão (ou a qualquer momento), o operador pode acessar dois relatórios principais:

### 7.1 Relatório de contas fechadas (pagas)

Exibe todas as contas liquidadas na sessão corrente. Informações por registro:

- Nome do atleta e do pai.
- Itens consumidos (por tipo de refeição).
- Valor total pago.
- Horário do fechamento.
- Total geral arrecadado no relatório.

### 7.2 Relatório de contas em aberto

Exibe todos os clientes com consumo registrado e conta não paga. Informações por registro:

- Nome do atleta e do pai.
- Itens consumidos até o momento.
- Valor total em aberto.
- Total geral pendente no relatório.

### 7.3 Ações nos relatórios

- Exportar lista (formato a definir na próxima versão).
- Acessar o fechamento de conta diretamente pelo relatório de abertos.
- Reenviar comprovante por e-mail (pelo relatório de fechadas).

---

## 8. Requisitos não funcionais

| ID | Requisito | Descrição |
| -- | --------- | --------- |
| RNF-01 | Usabilidade | Interface simples e operável em tablet/smartphone em ambiente de evento |
| RNF-02 | Desempenho | Registro de pedidos em menos de 2 segundos |
| RNF-03 | Confiabilidade | Sem perda de dados ao reiniciar o caixa; histórico de sessão preservado até o reset intencional |
| RNF-04 | Notificação | Envio de e-mail de comprovante em até 1 minuto após confirmação |
| RNF-05 | Segurança | Acesso restrito ao operador autenticado; dados de clientes protegidos |
| RNF-06 | Escalabilidade | Suporte a pelo menos 200 clientes por sessão sem degradação |

---

## 9. Regras de negócio

Todas as regras de negócio (incluindo RN-01 a RN-10 e regras complementares dos módulos) estão centralizadas em:

**[REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md)**

---

## 10. Fluxo geral do sistema

### Fase 1 — Configuração inicial (antes do evento)

- Cadastro de atletas com nome, **modalidade** (softball/baseball), **categoria esportiva**, idade e e-mail do pai.
- Cadastro de pais vinculados a cada atleta.
- Cadastro de preços por modalidade (softball/baseball), categoria esportiva do atleta, pai/responsável correspondente e valor de refeição avulsa.
- Cadastro de itens fixos (refrigerante, cerveja, água) com valores.

### Fase 2 — Operação do caixa (durante o evento)

- Operador seleciona o tipo de refeição ativo.
- Seleciona o cliente na lista e registra os itens pedidos.
- Repete o processo para todos os clientes.

### Fase 3 — Fechamento de conta (por cliente)

- Operador acessa o cliente, visualiza o resumo consolidado e confirma o pagamento.
- Sistema registra como pago e dispara o e-mail de comprovante.

### Fase 4 — Fechamento do caixa (encerramento da sessão)

- Operador consulta os relatórios de contas pagas e em aberto.
- Encerra a sessão, reiniciando a tela inicial.

---

## 11. Considerações para próximas versões

- Adicionar outros meios de pagamento (dinheiro, cartão, crédito interno).
- Exportação de relatórios em PDF e Excel.
- Histórico de sessões anteriores.
- Aplicativo mobile dedicado com modo offline.
- Integração com sistema de gestão de eventos.
- Painel administrativo para gestão de preços e categorias.

---

*Fim do documento — PRD Sistema PDV de Refeições v1.0.*
