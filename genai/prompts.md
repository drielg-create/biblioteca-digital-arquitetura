# Registro de uso de GenAI

Ferramenta: **Claude (Opus 5.5)**, usado via Claude Code no VS Code.
Data: 13/10/2026.

O processo teve duas etapas: primeiro uma geração direta a partir de um prompt curto (saída `v0`), depois uma revisão crítica guiada por prompts de refinamento. As saídas brutas estão em [`saida-original/`](saida-original/) e as versões finais em [`../diagramas/`](../diagramas/).

## Prompt 1 — diagrama estrutural (gerou `containers-v0.mmd`)

```text
Gere, em Mermaid, um diagrama de containers no estilo C4 para um sistema de
biblioteca digital que gerencia catálogo, empréstimos, reservas e multas.
Atores: leitor e bibliotecário. Inclua integrações externas relevantes.
```

## Prompt 2 — diagrama comportamental (gerou `sequencia-emprestimo-v0.mmd`)

```text
Gere, em Mermaid, um diagrama de sequência da jornada crítica "leitor solicita
empréstimo de um livro" usando os containers do diagrama anterior.
```

## Prompt 3 — refinamento estrutural

```text
Revise o diagrama de containers considerando estas restrições: equipe de 4
desenvolvedores, orçamento público limitado, autenticação via SSO institucional,
acervo físico e de e-books com DRM, conformidade com a LGPD. Use rótulos em
português, informe tecnologia e protocolo em cada relação e use sintaxe
flowchart (a sintaxe C4 do Mermaid é experimental e renderiza mal no GitHub).
Diferencie visualmente pessoas, containers, armazenamento e sistemas externos.
```

## Prompt 4 — refinamento comportamental

```text
Revise o diagrama de sequência: inclua autenticação, os caminhos de falha
(leitor inelegível, item indisponível, falha da distribuidora de e-books),
trate a concorrência de dois leitores pedindo o último exemplar, garanta
idempotência no POST e mova a notificação para fora da transação usando
outbox. Diferencie e-book de livro físico.
```

## Observação

Os prompts 3 e 4 trazem decisões tomadas por mim, autor do projeto, após analisar a saída `v0`. A GenAI aplicou essas decisões, mas não as originou. A justificativa de cada uma está na seção **Decisões e ajustes** do [README](../README.md#5-decisões-e-ajustes-sobre-a-saída-da-genai).
