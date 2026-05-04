# Primeira POC — Briefing para o time júnior

**Projeto de referência:** Sistema PDV de Refeições (eventos esportivos — PlayBall).  
**Documentação de produto:** [README.md](README.md) · **Regras de negócio:** [REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md)  
**Estudo e foco (trilha, erros comuns, links):** [DICAS_E_ORIENTACOES_ESTUDO.md](DICAS_E_ORIENTACOES_ESTUDO.md)

---

## 1. Objetivo deste exercício

Projetar e implementar uma **mini aplicação** (prova de conceito) inspirada no PDV de refeições descrito na documentação do repositório. O foco é **aprendizado, organização de código e comunicação**: vocês têm **liberdade total** para decidir **escopo**, **fluxos**, **telas** e **prioridades** — desde que respeitem os **requisitos técnicos obrigatórios** abaixo.

A POC não precisa cobrir o sistema inteiro do PRD; pode ser um **recorte** bem definido (por exemplo: apenas cadastro de clientes + um tipo de refeição + um pedido simples, ou só dashboard de relatório simulado). O importante é que o que entregar seja **coerente**, **simples de rodar** e **bem explicado por escrito**.

---

## 2. O que vocês devem fazer (missão)

1. **Ler** o [README.md](README.md) e, se necessário, [REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md) para entender o domínio (clientes, modalidades softball/baseball, pedidos, conceito de sessão de caixa, etc.).
2. **Definir** em conjunto o escopo da mini POC: uma frase de visão + lista do que está **dentro** e **fora** do escopo.
3. **Implementar** a solução em **Python**, com interface **interativa em Dash**.
4. **Aplicar programação orientada a objetos** na modelagem (domínio, serviços ou repositórios — vocês escolhem o desenho).
5. **Documentar** o projeto de forma que outra pessoa consiga instalar, rodar e entender as decisões.

---

## 3. Liberdade criativa (o que é de vocês)

- Quantas telas, quais fluxos e quais dados mockados ou em memória.
- Se simulam e-mail, PIX ou apenas registram “conta paga” em texto.
- Nomes de pastas, convenções internas e granularidade das classes.
- Uso de dados fictícios para eventos, atletas e cardápio.

**Única condição:** no README da POC (ou neste documento, em seção própria), deixem explícito **o que a POC faz** e **o que de propósito não foi feito** para esta primeira versão.

---

## 4. Requisitos técnicos obrigatórios

### 4.1 Python e programação orientada a objetos

- O núcleo da lógica (entidades, regras simples, agregação de pedidos, etc.) deve estar em **classes** com responsabilidades claras.
- Evitem colocar toda a lógica dentro dos callbacks do Dash; **separe** modelo/regra de apresentação.
- Exemplos do que pode ser OO (não é lista fechada — adaptem ao seu desenho): `Cliente`, `Atleta`, `ItemCardapio`, `Pedido`, `SessaoCaixa`, `Precificacao`, serviços do tipo `RegistrarPedido`, etc.

### 4.2 Dash interativo

- A interface principal deve ser uma app **Dash** (Plotly Dash), com **callbacks** que respondem a ações do usuário (cliques, seleções, formulários).
- A experiência deve ser **interativa**, não uma página estática gerada uma única vez sem reação a inputs.

### 4.3 HTML, CSS e JavaScript

O Dash já renderiza HTML e permite estilização e comportamento extra:

- **CSS:** use pasta `assets/` do Dash (por exemplo `assets/style.css`) para organizar estilos; podem complementar com classes nos componentes Dash (`className`).
- **HTML:** podem usar `html.*` do Dash; se fizer sentido, componentes com trechos HTML específicos são válidos.
- **JavaScript:** **opcional**, mas encorajado quando agregar clareza — por exemplo **callbacks do lado do cliente** (`dash_clientside`) para pequenas interações ou validações visuais. Não é obrigatório um SPA separado; integrem ao app Dash de forma simples.

Em resumo: **Python + Dash como espinha dorsal**; HTML/CSS (e JS se útil) como camada de apresentação alinhada à documentação que vocês mesmos escreverem.

### 4.4 Simplicidade e documentação

- **Simples:** poucos comandos para instalar e rodar (`requirements.txt` ou `pyproject.toml` + instruções claras).
- **Documentado:**
  - `README` na raiz da POC com: objetivo, como instalar, como executar, estrutura de pastas breve.
  - Comentários ou docstrings **onde ajudarem** (sem excesso de óbvio).
  - Opcional: diagrama simples (fluxo ou classes) em Markdown ou imagem na pasta da POC.

---

## 5. Entregáveis sugeridos

| Entregável | Descrição |
| ---------- | --------- |
| Código fonte | Projeto Python organizado (módulos/pacotes ao critério do time). |
| Dependências | Arquivo de dependências travando versões razoáveis (evitar “funciona na minha máquina” sem versão). |
| README | Instalação, execução, escopo da POC e decisões de design. |
| Demonstração | Breve roteiro no README (“clique aqui, espere isto”) ou gif/link gravado — opcional mas valorizado. |

---

## 6. Critérios de avaliação (orientação para o time)

- **Clareza:** outra pessoa roda e entende o fluxo principal em poucos minutos.
- **OO:** classes com papéis definidos; não um único arquivo gigante sem separação.
- **Dash:** uso real de interatividade (callbacks ligados a controles).
- **Documentação:** README honesto sobre limitações e próximos passos.
- **Alinhamento solto ao domínio:** pelo menos algum conceito do PDV (cliente, pedido, refeição, modalidade, etc.) aparece de forma reconhecível.

---

## 7. Referências rápidas no repositório

- Dicas de estudo e ordem de aprendizado (para não se perder): [DICAS_E_ORIENTACOES_ESTUDO.md](DICAS_E_ORIENTACOES_ESTUDO.md)
- Produto e fluxos: [README.md](README.md)
- Regras de negócio: [REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md)
- POC estática/HTML existente (referência visual ou contraste — **não é obrigatório** reutilizar): pasta `Documentação/POC-1/` se aplicável ao que vocês forem construir.

---

## 8. Próximo passo para vocês (checklist inicial)

- [ ] Ler a documentação do produto e escolher o **recorte** da POC.
- [ ] Esboçar **3 a 5 classes** principais e como conversam.
- [ ] Criar o projeto Dash mínimo que roda uma página com um input e um callback.
- [ ] Iterar até ter um fluxo completo do recorte escolhido.
- [ ] Fechar com README e revisão entre pares.

---

*Boa POC — priorizem algo que funcione ponta a ponta e que vocês consigam explicar com orgulho em dez minutos.*
