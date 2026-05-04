# Dicas e orientações de estudo — time júnior (POC PDV)

Este arquivo existe para **reduzir ansiedade e dispersão**: uma ordem razoável de estudo, onde buscar ajuda e como saber quando “já está bom o suficiente” para avançar.

**Leiam primeiro:** [PRIMEIRA_POC.md](PRIMEIRA_POC.md) (briefing da POC).

---

## 1. Como estudar sem se perder

### 1.1 Uma trilha por vez

Não tentem dominar “Python + OO + Dash + CSS + JS + domínio PDV” no mesmo dia. Sugestão de **sequência**:

1. **Domínio (produto)** — 1 leitura calmada do [README.md](README.md); anotem em 5 bullets “o que o sistema faz”. Só voltem ao [REGRAS_NEGOCIO.md](REGRAS_NEGOCIO.md) quando precisarem de detalhe (preços, TBol, sessão de caixa).
2. **Python básico sólido** — funções, listas/dicts, módulos, `if`/`for`, tratamento simples de erro (`try`/`except` só onde fizer sentido).
3. **Orientação a objetos** — classes, `__init__`, métodos, quando usar composição (“Pedido **tem** itens”) vs herança moderada.
4. **Dash mínimo viável** — layout + **um** callback que altera algo na tela.
5. **Callbacks extras** — formulários, botões, estados (`dcc.Store`), depois organização em mais arquivos.
6. **CSS em `assets/`** — depois que a app já reage a cliques; estética não deve bloquear o primeiro fluxo funcionando.
7. **JavaScript / clientside** — só se sobrou tempo e há um ganho claro (validação visual, animação leve).

### 1.2 Definição de “pronto por hoje”

Encerre o dia com **algo executável**: mesmo que feio, “rodei `python app.py` e o botão mudou um texto”. Isso evita a sensação de estudar sem entregar.

### 1.3 Limite de tempo ao pesquisar

Se travarem mais de **45–60 minutos** no mesmo erro:

- Leiam a **mensagem de erro completa** (últimas linhas do terminal).
- Busquem com palavras exatas do erro + “dash” ou “python”.
- Peçam ajuda a colega ou mentor **com**: o que queriam fazer, o que clicaram/rodaram, e o **texto do erro** (print ou cópia).

Ficar horas no mesmo ponto sem registrar o erro costuma ser desperdício.

---

## 2. Orientação a objetos (o que realmente importa na POC)

- **Classes pequenas:** melhor várias classes claras do que uma “God class” com tudo.
- **Domínio primeiro:** `Cliente`, `Pedido`, `LinhaPedido` podem existir **sem** Dash; testem criando objetos no interpretador Python ou num `if __name__ == "__main__":` rápido.
- **Separação:** callbacks do Dash chamam métodos como `servico.adicionar_item(...)` em vez de 80 linhas de lógica dentro do callback.
- **Dataclasses** (`@dataclass`) são opcionais mas ajudam a padronizar dados; não são obrigatórias.

Quando duvidarem “isso é OO suficiente?”: se outra pessoa lê o código e entende **quem é responsável por quê**, está no caminho certo.

---

## 3. Dash — foco para não se perder

### 3.1 Conceitos que vocês precisam dominar cedo

- **Layout:** árvore de componentes (`html.Div`, `dcc.Dropdown`, `dbc.Button` se usarem Dash Bootstrap Components, etc.).
- **IDs:** cada componente que participa de callback precisa de `id` único e estável.
- **Callbacks:** `@app.callback` ligando **Outputs** e **Inputs**; entender `prevent_initial_call` só quando necessário.
- **Estado na sessão:** para POC, `dcc.Store` em memória costuma bastar; não precisam de banco na primeira versão.

### 3.2 Erros comuns (e o que checar)

| Sintoma | O que verificar |
| ------- | ---------------- |
| “Duplicate callback outputs” | Dois callbacks alterando o mesmo `Output`. |
| “Nonexistent object was used in an Input” | `id` errado ou componente não está no layout na hora do callback. |
| Callback não dispara | `Input` não mudou; conferir `n_clicks` vs valor de dropdown. |
| Página em branco | Erro no terminal ao iniciar; conferir imports e sintaxe. |

### 3.3 Documentação oficial (referências)

- **Dash:** [Plotly Dash Documentation](https://dash.plotly.com/)
- **Tutorial layouts e callbacks:** seções *Layout* e *Basic Callbacks* do site acima.
- **Arquivo estático CSS:** [External Stylesheets / assets folder](https://dash.plotly.com/external-resources) (pastas `assets/`).

Priorizem sempre a documentação oficial antes de tutoriais aleatórios com versões antigas.

---

## 4. HTML e CSS (no contexto Dash)

- **HTML:** no Dash vocês montam estrutura com `dash.html`; não precisam escrever arquivo `.html` gigante à mão a menos que decidam isso como time.
- **CSS:** começuem com poucas regras — cores, margens, fonte — em `assets/style.css`; usem `className` nos componentes.
- **Responsividade:** útil mas não bloqueante na POC; primeiro fluxo funcional, depois “bonito no celular”.

---

## 5. JavaScript (opcional)

- Na POC, JS aparece sobretudo via **callbacks clientside** da Plotly ([Clientside Callbacks](https://dash.plotly.com/clientside-callbacks)).
- Se ninguém do time tiver familiaridade, **deixem JS para o fim** ou não usem: interatividade com callbacks **Python** já atende o briefing.

---

## 6. Trabalho em equipe sem caos

- **Um branch ou pasta por experimento** se usarem Git; evitem “todos editando o mesmo arquivo gigante” sem combinar.
- **Combinem o recorte da POC por escrito** antes de codar três fluxos diferentes ao mesmo tempo.
- **Revisão entre pares:** 15 minutos em que uma pessoa explica a tela enquanto a outra clica — revela buracos na documentação.

---

## 7. Saúde mental e expectativa

- A primeira POC **não** precisa ser bonita nem completa; precisa ser **honesta** (README diz o que faz e o que não faz).
- Comparar com projetos gigantes da internet desmotiva; comparem com **o briefing** e com **o ontem de vocês mesmos**.

---

## 8. Checklist rápido “estou perdido — por onde começo agora?”

- [ ] Eu sei qual é **uma única** história de usuário que nossa POC demonstra? (ex.: “operador registra um pedido mock”.)
- [ ] Consigo desenhar **no papel** 3 caixinhas (classes) e setas entre elas?
- [ ] Meu Dash abre no navegador sem erro?
- [ ] Existe **um** callback que muda algo na tela?
- [ ] O README diz como rodar em **dois comandos** ou menos?

Se algum item for “não”, esse é o próximo passo — não abram um quarto tópico novo até destravar isso.

---

*Última dica: estudem como se fossem ensinar o colega na segunda-feira — o que não conseguem explicar em uma frase, ainda não está claro o suficiente.*
