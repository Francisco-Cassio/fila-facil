# 02 — Incremento 1: implementar emitirSenha

- **Data:** 2026-11-06
- **Autoria:** Francisco de Cássio da Silva Mourão Júnior (@Francisco-Cassio)
- **Ferramenta:** Antigravity
- **Modelo:** Gemini 4 Argon (Medium)
- **Trilha:** nuvem (Rota A — Agente com ferramentas)
- **Requisito ou critério alvo:** RF-02 (emissão de senhas sequenciais sem alterar atendimento)

## O que foi pedido

```text
Implemente somente o corpo de emitirSenha em labs/lab-02-fila-facil/src/fila.js,
conforme RF-02. Preserve o restante do arquivo, a interface e os testes.
Não implemente as outras duas funções agora. Explique o efeito em cada campo do estado.
Se Node já estiver disponível, execute node labs/lab-02-fila-facil/tests/executar.mjs
na raiz e relate a saída real. Se não estiver, eu executarei a suíte no navegador;
não instale dependências nem declare testes aprovados sem execução.
```

## Contexto fornecido

Arquivos lidos na etapa 01 (`AGENTS.md`, `ESPECIFICACAO.md`, `src/fila.js`) e linha de base (`6 aprovados · 18 falhas`).

## O que veio

O agente implementou apenas `emitirSenha(estado)` em `src/fila.js` (inserindo `estado.proximaSenha` ao final de `estado.aguardando`, incrementando `estado.proximaSenha += 1` e retornando o número emitido, mantendo `atual` e `totalChamadas` intactos). Executou `node labs/lab-02-fila-facil/tests/executar.mjs`, obtendo `10 aprovados · 14 falhas · 24 testes`.

## O que eu fiz com isso

Aceitei como veio após conferir o `git diff -- labs/lab-02-fila-facil/src/fila.js` e confirmar que `chamarProxima` e `reiniciarFila` permaneceram inalteradas nesta etapa.
