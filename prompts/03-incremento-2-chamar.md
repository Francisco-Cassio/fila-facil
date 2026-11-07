# 03 — Incremento 2: implementar chamarProxima

- **Data:** 2026-11-06
- **Autoria:** Francisco de Cássio da Silva Mourão Júnior (@Francisco-Cassio)
- **Ferramenta:** Antigravity
- **Modelo:** Gemini 4 Argon (Medium)
- **Trilha:** nuvem (Rota A — Agente com ferramentas)
- **Requisito ou critério alvo:** RF-03 (chamada FIFO e contagem efetiva) e RF-04 (fila vazia preserva estado)

## O que foi pedido

```text
Agora implemente somente chamarProxima em labs/lab-02-fila-facil/src/fila.js.
Cumpra RF-03 e RF-04: atender FIFO, retirar da espera, atualizar a senha atual e
contar chamadas efetivas. Fila vazia retorna null e preserva todo o estado.
Preserve emitirSenha, a interface, reiniciarFila e os testes. Verifique pelo caminho
disponível e explique como tratou o caso vazio. Não acrescente prioridade ainda.
```

## Contexto fornecido

Estado de `src/fila.js` após o Incremento 1 (`10 aprovados · 14 falhas · 24 testes`) e especificação RF-03 / RF-04.

## O que veio

O agente implementou `chamarProxima(estado)` verificando primeiro `if (estado.aguardando.length === 0) return null;` (preservando `atual` e `totalChamadas` quando vazia) e, havendo espera, removendo a primeira senha com `estado.aguardando.shift()`, atualizando `estado.atual`, incrementando `estado.totalChamadas += 1` e retornando a senha chamada. A execução real da suíte passou para `20 aprovados · 4 falhas · 24 testes`.

## O que eu fiz com isso

Aceitei como veio após conferir no `git diff` e na suíte que os testes de emissão (RF-02), chamada FIFO (RF-03) e fila vazia (RF-04) passaram integralmente.
