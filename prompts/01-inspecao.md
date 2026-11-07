# 01 — Inspeção inicial do contrato e plano em incrementos (sem edição)

- **Data:** 2026-11-06
- **Autoria:** Francisco de Cássio da Silva Mourão Júnior (@Francisco-Cassio)
- **Ferramenta:** Antigravity
- **Modelo:** Gemini 4 Argon (Medium)
- **Trilha:** nuvem (Rota A — Agente com ferramentas)
- **Requisito ou critério alvo:** RF-01 a RF-07 (inspeção de contrato e planejamento)

## O que foi pedido

```text
Vamos trabalhar somente no Lab 02 — Fila Fácil.
Leia AGENTS.md da raiz, labs/lab-02-fila-facil/AGENTS.md, a especificação completa
e src/fila.js desse lab. Ainda não edite arquivos.
Resuma o contrato, identifique as três funções pendentes e proponha três incrementos.
Explique como verificar cada um e quais arquivos você não pode alterar.
Se tiver ferramentas, mostre as leituras reais. Não imprima chamadas fictícias.
```

## Contexto fornecido

Repositório clonado com `AGENTS.md` (raiz), `labs/lab-02-fila-facil/AGENTS.md`, `labs/lab-02-fila-facil/ESPECIFICACAO.md`, `labs/lab-02-fila-facil/src/fila.js` e saída da linha de base (`6 aprovados · 18 falhas · 24 testes`).

## O que veio

O agente realizou a leitura real dos 4 arquivos sem editar o código, resumiu o contrato de `globalThis.FilaFacil`, identificou as três funções pendentes (`emitirSenha`, `chamarProxima` e `reiniciarFila`), propôs os três incrementos isolados com suas metas de verificação (`10/24`, `20/24` e `24/24`) e listou os arquivos protegidos (`tests/`, `index.html`, `src/app.js`, `src/estilo.css`, `ESPECIFICACAO.md`, `AGENTS.md` e `labs/lab-01-validador-senha/`).

## O que eu fiz com isso

Aceitei o plano após conferir que nenhuma edição prematura foi feita (`git status --short` sem modificações em código) e que o escopo se manteve restrito a `src/fila.js`.
