# Evidências — Lab 02: Fila Fácil (Fluxo Básico)

- **Dupla / Autoria:** Francisco de Cássio da Silva Mourão Júnior (@Francisco-Cassio)
- **Data:** 2026-11-06
- **Rota / Trilha:** Rota A — Agente com ferramentas (nuvem)
- **Ferramenta e modelo:** Antigravity · Gemini 4 Argon (Medium)
- **Ambiente:** Windows, Git 2.55.0, Node v24.20.0, uv 0.13.6

---

## 1. Ponto de partida e Resumo dos Testes (Inicial, Incrementos e Final)

Comando de verificação executado na raiz do repositório:
```bash
node labs/lab-02-fila-facil/tests/executar.mjs
```

| Métrica / Etapa | Valor / Resultado Real |
|---|---|
| **Testes passando antes (Linha de base)** | `6 aprovados · 18 falhas · 24 testes` |
| **Após Incremento 1 (`emitirSenha`)** | `10 aprovados · 14 falhas · 24 testes` |
| **Após Incremento 2 (`chamarProxima`)** | `20 aprovados · 4 falhas · 24 testes` |
| **Testes passando depois (`reiniciarFila`)** | `24 aprovados · 0 falhas · 24 testes` |
| **Rodadas até passar** | 4 etapas planejadas (1 inspeção + 3 incrementos) |
| **Correções manuais necessárias no código** | 0 (código validado a cada incremento via suíte e `git diff`) |

### Saída real da Linha de Base (antes da implementação)
```text
PASSOU | RF-01 · estado inicial completo
PASSOU | RF-07 · estados iniciais independentes
PASSOU | RF-06 · ausência de senha
PASSOU | RF-06 · senha com três dígitos
PASSOU | RF-06 · senha com dois algarismos
PASSOU | RF-06 · não truncar após 999
FALHOU | RF-02 · primeira emissão retorna 1 | LAB02_PENDENTE: emitirSenha
...
6 aprovados · 18 falhas · 24 testes
```

### Saída real Final (após os 3 incrementos)
```text
PASSOU | RF-01 · estado inicial completo
PASSOU | RF-07 · estados iniciais independentes
PASSOU | RF-06 · ausência de senha
PASSOU | RF-06 · senha com três dígitos
PASSOU | RF-06 · senha com dois algarismos
PASSOU | RF-06 · não truncar após 999
PASSOU | RF-02 · primeira emissão retorna 1
PASSOU | RF-02 · emissão atualiza a fila
PASSOU | RF-02 · emissão avança a numeração
PASSOU | RF-02 · emitir preserva atendimento e contador
PASSOU | RF-02 · numeração continua após chamada
PASSOU | RF-03 · chamada retorna a primeira senha
PASSOU | RF-03 · remove somente a primeira da espera
PASSOU | RF-03 · atual acompanha a última chamada
PASSOU | RF-03 · conta somente chamadas efetivas
PASSOU | RF-03 · chamar não avança proximaSenha
PASSOU | RF-04 · chamar fila inicialmente vazia retorna null
PASSOU | RF-04 · fila vazia preserva todos os campos
PASSOU | RF-03 · FIFO com emissão entre chamadas
PASSOU | RF-05 · reinício restaura o mesmo objeto
PASSOU | RF-05 · primeira emissão após reinício
PASSOU | RF-05 · reiniciar duas vezes é válido
PASSOU | RF-07 · operar uma fila não modifica outra
PASSOU | RF-02/03 · mil emissões e chamadas sem duplicação
24 aprovados · 0 falhas · 24 testes
```

---

## 2. Roteiro Visual e Capturas do Protótipo

Servidor local para conferência visual no navegador:
```bash
uv run python -m http.server 8000 --bind 127.0.0.1 -d labs/lab-02-fila-facil
```
- **Aplicação:** `http://127.0.0.1:8000/`
- **Testes:** `http://127.0.0.1:8000/tests/`

| Ação | Resultado Esperado | Status |
|---|---|---|
| Recarregar a aplicação | `"—"`, espera 0 e chamadas 0 | Conferido |
| Emitir três senhas | `N001, N002, N003`, sem chamada automática | Conferido |
| Chamar uma | `N001` atual; `N002` e `N003` aguardando; total 1 | Conferido |
| Emitir outra | `N004` entra ao fim da espera | Conferido |
| Chamar até esvaziar | Ordem `N002, N003, N004`; total 4 | Conferido |
| Chamar vazia | Preserva `N004` e total 4; mostra aviso `"Não há senhas aguardando."` | Conferido |
| Cancelar reinício | Nenhum dado muda | Conferido |
| Confirmar reinício | Limpa tudo; próxima emissão `N001` | Conferido |
| Usar Tab e Enter | Botões acessíveis por teclado; foco visível (`outline` laranja) | Conferido |
| Recarregar ou abrir outra aba | Nova sessão vazia; abas não sincronizam | Conferido |

---

## 3. Arquivos Alterados e Decisão de Implementação

### Arquivos alterados
- **Código:** somente `labs/lab-02-fila-facil/src/fila.js` (`git diff -- labs/lab-02-fila-facil/tests` permanece vazio).
- **Registros:** `labs/lab-02-fila-facil/prompts/01-inspecao.md` a `04-incremento-3-reiniciar.md` e `labs/lab-02-fila-facil/evidencias/resultado.md`.

### O que eu entendi do código e Decisão de Implementação explicada pela dupla
- **`emitirSenha(estado)` (RF-02):** Lê o número disponível em `estado.proximaSenha`, adiciona esse número ao fim do array `estado.aguardando` com `.push()`, incrementa `estado.proximaSenha += 1` e devolve o número emitido. Não toca em `estado.atual` nem em `estado.totalChamadas`, pois a chegada de uma pessoa na fila é independente de quem está sendo atendido no guichê.
- **`chamarProxima(estado)` (RF-03 e RF-04):** Primeiro verifica se `estado.aguardando.length === 0`. Se estiver vazia, retorna `null` imediatamente sem alterar nenhum campo do estado (preservando a última senha em `estado.atual` e o contador `estado.totalChamadas`, conforme RF-04). Caso haja senhas esperando, retira a primeira da fila com `.shift()` (ordem FIFO), grava esse número em `estado.atual`, soma `1` em `estado.totalChamadas` e retorna a senha chamada.
- **`reiniciarFila(estado)` (RF-05):** Reatribui diretamente no próprio objeto `estado` recebido os quatro valores iniciais (`proximaSenha = 1`, `aguardando = []`, `atual = null`, `totalChamadas = 0`). A decisão de mutar o objeto recebido in-place (em vez de retornar um novo objeto `{...}`) é essencial porque `src/app.js` e a suíte de testes guardam a referência original criada por `criarEstado()`.

---

## 4. Intervenção Humana, Revisão e O que precisou de retrabalho

- **Controle de escopo em incrementos:** Conduzimos o agente passo a passo (inspeção sem edição → `emitirSenha` → `chamarProxima` → `reiniciarFila`), validando a contagem exata da suíte (`6/24` → `10/24` → `20/24` → `24/24`) e o `git diff` a cada turno.
- **Preservação do repositório da disciplina:** Ao configurar regras locais de ignore para arquivos de IDE/agentes, movemos as regras extras para `.git/info/exclude` e restauramos o `.gitignore` original da raiz para garantir que `git status --short` exibisse estritamente `labs/lab-02-fila-facil/src/fila.js`, `prompts/` e `evidencias/`, conforme exigido no Passo 10 do tutorial.

---

## 5. Dúvidas e Limitações Restantes

- **Limites arquiteturais (RF-07):** O estado vive apenas em memória na aba atual do navegador (`const estado = fila.criarEstado()` em `src/app.js`). Recarregar a página zera a fila, e duas pessoas abrindo a mesma URL pública no GitHub Pages têm filas independentes, pois não há backend, API ou banco de dados.
- **Próximo passo:** Publicação da entrega verificável no GitHub Pages com documentação na Issue (Aula 07) e/ou evolução da fila com prioridade administrativa em branch separada (`EXERCICIOS.md`).
