# Fila Fácil

Protótipo didático de recepção para emissão e chamada de senhas por ordem de chegada (**FIFO**), desenvolvido e verificado em incrementos supervisionados com apoio de agente de IA.

---

## 📋 Ficha do Projeto

- **Objetivo:** Protótipo didático de emissão e chamada de senhas em ordem FIFO (`RF-01` a `RF-07`).
- **Origem:** Lab 02 da disciplina **TEC.1053 — Tópicos Especiais em Programação** (ADS IV · IFPI · Prof. Aislan Rafael), [github.com/aislanifpi/tec1053](https://github.com/aislanifpi/tec1053).
- **Autor:** Francisco de Cássio da Silva Mourão Júnior ([@Francisco-Cassio](https://github.com/Francisco-Cassio))

---

## 🔗 Links Públicos

| Recurso | Endereço |
|---|---|
| **Aplicação pública (GitHub Pages)** | <https://francisco-cassio.github.io/fila-facil/> |
| **Suíte de Testes (24 testes no navegador)** | <https://francisco-cassio.github.io/fila-facil/tests/index.html> |
| **Tarefa e Evidências (Issue #1)** | <https://github.com/Francisco-Cassio/fila-facil/issues/1> |

---

## 🚀 Como Executar Localmente

Não é necessário instalar pacotes, frameworks ou banco de dados (HTML, CSS e JavaScript nativos):

1. **Direto pelo navegador:**
   Abra os arquivos [`index.html`](index.html) (aplicação) e [`tests/index.html`](tests/index.html) (suíte de 24 testes).
2. **Com servidor HTTP local (opcional):**
   ```bash
   uv run python -m http.server 8000 --bind 127.0.0.1
   ```
   - Aplicação: `http://127.0.0.1:8000/`
   - Testes: `http://127.0.0.1:8000/tests/`
3. **Execução da suíte via Node.js no terminal (opcional, Node 18+):**
   ```bash
   node tests/executar.mjs
   ```

---

## ⚙️ Contrato e Estrutura do Projeto

```text
fila-facil/
├── index.html          # Interface da recepção e diálogo de confirmação
├── ESPECIFICACAO.md    # Contrato normativo (RF-01 a RF-07)
├── src/
│   ├── fila.js         # Regras de domínio (criarEstado, formatarSenha, emitirSenha, chamarProxima, reiniciarFila)
│   ├── app.js          # Integração de eventos da interface com globalThis.FilaFacil
│   └── estilo.css      # Estilos e indicador de foco acessível (:focus-visible)
├── tests/              # Suíte oficial de 24 testes (intacta)
├── prompts/            # Registro dos prompts enviados em cada incremento
└── evidencias/         # Relatório de verificação inicial, intermediária e final
```

---

## ⚠️ Limites Conhecidos do Protótipo

- **Uma fila por aba (`RF-07`):** O estado é mantido exclusivamente em memória na sessão da aba aberta.
- **Sem persistência ou sincronização:** Recarregar a página reinicia a fila do zero, e abrir a URL em outra aba ou outro computador cria uma fila independente (não há backend, API ou `localStorage`).
- **Dados fictícios:** Utiliza apenas senhas sequenciais geradas na hora (`N001`, `N002`...), sem coleta de dados pessoais.
