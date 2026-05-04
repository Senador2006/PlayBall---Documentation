# Regras de negócio — Sistema PDV de Refeições

Documento consolidado das regras de negócio do **Sistema PDV de Refeições** (eventos esportivos). Versão alinhada ao PRD v1.0.

---

## 1. Categorias, faixa etária e precificação

- O sistema deve suportar **modalidades** (**softball** e **baseball**), **categorias esportivas** com faixas etárias distintas por modalidade e **preços pré-cadastrados** por combinação aplicável (atleta, pai, avulso).
- O cadastro do atleta deve registrar **modalidade** e **categoria esportiva**, para aplicar faixa etária e tabela de preços corretas.

### Softball — categorias e idades

| Categoria | Faixa etária | Observação |
| --------- | ------------ | ---------- |
| TBol | Até 9 anos | Abaixo de 5 anos: isento (sem lançamento de refeição de atleta nesta categoria) |
| Sub 11 | Até 11 anos | — |
| Sub 13 | Até 13 anos | — |
| Sub 16 | Até 16 anos | — |
| Sub 19 | 17 a 19 anos | — |
| Sub 23 | 20 a 23 anos | — |
| Adulto | Acima de 23 anos | — |

### Baseball — categorias e idades

| Categoria | Faixa etária |
| --------- | ------------ |
| TBol | 5 a 8 anos |
| Pré-infantil | 9 a 10 anos |
| Infantil | 11 a 12 anos |
| Pré-júnior | 13 a 14 anos |
| Júnior | 15 a 16 anos |
| Juvenil | 17 a 18 anos |
| Sub 23 | 19 a 23 anos |
| Adulto | Acima de 23 anos |

- **Atletas:** em geral **pagam o valor próprio da categoria** (configurado por modalidade + categoria). **TBol (softball e baseball):** crianças **abaixo de 5 anos** não pagam refeição de atleta nessa categoria (**isento**; sem lançamento), alinhado à **RN-01**.
- **Pais e responsáveis:** cada categoria de atleta (por modalidade) tem valor correspondente para pais/responsáveis, **configurado previamente**. O pai é **vinculado ao atleta** no cadastro, permitindo visualização cruzada dos pedidos.
- **Parentes e amigos:** pagam valor de **refeição avulsa**.
- **Isento:** crianças **abaixo de 5 anos** e **treinadores (senseis)** não geram lançamento de refeição (conforme política do evento).

---

## 2. Itens fixos, disponibilidade e “Diversos”

- Itens como **refrigerante, cerveja, água** têm **valor fixo** conforme cadastro (ex.: cerveja apenas para adultos).
- **Refeição (atleta/pais):** valor **pré-cadastrado por categoria**, para atletas e pais.
- **Refeição avulsa:** para parentes e amigos, valor **pré-cadastrado**.
- **Cadastrar Diversos (pré-evento na sessão):**
  - Um mesmo item pode estar vinculado a **vários tipos de refeição** (seleção múltipla, inclusive todos).
  - O valor é configurado no cadastro, mas **pode ser alterado** para itens “Diversos” **no momento do pedido**.
  - **Ao fechar o caixa**, todos os itens cadastrados em “Diversos” são **removidos** e a tela é reiniciada.
- **Item “Diversos” no pedido (ato do pedido):**
  - Operador informa **nome/descrição** e **valor unitário** na hora.
  - O item vale **apenas para aquele pedido**, sem alterar o cadastro geral.

---

## 3. Sessão, caixa e persistência

- **Fechamento do caixa** deve:
  - Limpar **todos os pedidos e consumos** da sessão.
  - Remover os itens “Diversos” cadastrados **nessa sessão**.
  - Voltar à **tela inicial** com tipos de refeição disponíveis.
  - **Manter intacto** o cadastro permanente de clientes (atletas e pais).
- **Sem perda de dados** ao reiniciar o caixa no sentido de **histórico de sessão preservado** até o reset intencional (conforme RNF de confiabilidade do PRD).

---

## 4. Pedidos e fluxo do operador

- **Um pedido só pode ser confirmado ou cancelado** antes de **iniciar outro cliente** (não é possível alternar cliente no meio de um pedido em aberto na UI).
- Durante a seleção de itens: **resumo em tempo real** (itens, quantidades, valores unitários, subtotal) e botões **Confirmar** e **Cancelar** visíveis.

---

## 5. Vinculação atleta — pai / responsável

- Cada atleta pode ter **um pai/responsável vinculado** (cadastro prévio).
- **Visualização cruzada:** ao abrir atleta ou pai, o sistema deve permitir ver consumo **consolidado** dos dois quando aplicável (fluxo descrito no PRD).
- **Fechamento de conta** pode ser **iniciado** a partir do **atleta** ou do **pai vinculado**.
- **Resumo consolidado para fechamento:** nomes, itens por tipo de refeição, quantidades, valores, total geral (atleta + pai).

---

## 6. Pagamento, comprovante e status de conta

- Na **versão inicial**, o único meio de pagamento aceito é **PIX**.
- A conta só é considerada **paga** após **confirmação manual do operador**.
- O **comprovante** é enviado **exclusivamente por e-mail** ao **pai/responsável**, com dados do evento, nomes, data/hora, itens detalhados e valor total.
- **Status:**
  - **Em aberto:** pedidos registrados, conta não paga — permitido adicionar itens e fechar conta.
  - **Paga:** pagamento confirmado — visualizar comprovante.
  - **Sem consumo:** sem pedidos na sessão — iniciar pedido.

---

## 7. Relatórios (ações de negócio)

- Relatório de **contas fechadas:** totais e detalhes por registro; **reenviar comprovante** por e-mail.
- Relatório de **contas em aberto:** totais pendentes; possibilidade de **acessar fechamento de conta** a partir do relatório.
- Exportação de lista: **formato a definir** em versão futura.

---

## 8. Resumo por ID (RN-01 a RN-10)

| ID    | Regra |
| ----- | ----- |
| RN-01 | Crianças abaixo de 5 anos não geram lançamento de refeição (isento), inclusive na categoria **TBol** do softball e do baseball. |
| RN-02 | Um pedido só pode ser confirmado ou cancelado antes de iniciar outro cliente. |
| RN-03 | O item Diversos tem valor e descrição definidos pelo operador no ato do pedido. |
| RN-04 | O fechamento do caixa reinicia a tela e remove itens Diversos da sessão. |
| RN-05 | O cadastro de clientes (atletas e pais) é persistente entre sessões. |
| RN-06 | A conta só é considerada paga após confirmação manual do operador. |
| RN-07 | O comprovante é enviado exclusivamente por e-mail ao pai/responsável. |
| RN-08 | A visualização cruzada (atleta/pai) exibe o consumo consolidado de ambos. |
| RN-09 | O fechamento da conta pode ser iniciado a partir do atleta ou do pai vinculado. |
| RN-10 | Na versão inicial, o único meio de pagamento aceito é PIX. |

---

*Fim do documento de regras de negócio — alinhado ao PRD Sistema PDV de Refeições v1.0.*
