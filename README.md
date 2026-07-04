# rag-local

Skill de [Claude Code](https://claude.com/claude-code) hecha por [PRYXIS](https://pryxis.es).

Le da a tu Claude Code local el contexto para **construir un asistente de IA privado
(RAG)** sobre los documentos de una empresa: responde en lenguaje natural citando la
fuente, controla la alucinacion y respeta permisos de acceso.

## Instalacion

```bash
git clone https://github.com/jordicabelloo/rag-local \
  ~/.claude/skills/rag-local
```

Claude Code cargara la skill cuando le pidas construir un RAG (o menciones "IA local",
"chat sobre documentos", "base vectorial", "embeddings", "on-premise").

## Uso

> Ayudame a montar un asistente RAG privado sobre la documentacion de mi empresa, con respuestas que citen la fuente.

## Contenido

- `SKILL.md` -- Definicion y workflow de construccion.
- `references/architecture.md` -- Fases de ingesta y consulta.
- `references/data-preparation.md` -- Fuentes, curacion y chunking.
- `references/retrieval-and-grounding.md` -- Embeddings, pgvector, reranking, grounding.
- `references/deployment-and-eval.md` -- Nube vs on-premise y evaluacion.
- `references/compliance.md` -- RGPD, no-entrenamiento y ACLs.

## Licencia

MIT. Uso libre. Hecho por PRYXIS.
