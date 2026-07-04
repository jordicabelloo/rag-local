---
name: rag-local
description: Usar cuando el usuario quiere construir, disenar o implementar un asistente de IA privado (RAG) sobre los documentos de una empresa, que responde en lenguaje natural citando la fuente y sin alucinar. Dispara con "RAG", "IA local", "asistente privado", "chat sobre mis documentos", "knowledge base con IA", "base de datos vectorial", "embeddings", "on-premise", "buscar en la documentacion de la empresa".
---

# RAG Local (asistente de IA privado sobre tus documentos)

## Overview

Esta skill le da a Claude el contexto para construir un sistema RAG (generacion
aumentada por recuperacion): un asistente privado, entrenado con los documentos de una
empresa, al que el equipo pregunta en lenguaje natural y que responde con precision
citando la fuente exacta. No es ChatGPT generico: responde SOLO desde los datos de la
empresa, controla la alucinacion y respeta permisos de acceso.

## When to Use

- El usuario quiere un asistente que responda desde los documentos privados de una empresa.
- El usuario habla de "RAG", "IA local", "chat sobre documentos", "knowledge base", "embeddings", "base vectorial", "on-premise".
- El usuario quiere que su equipo deje de perder horas buscando informacion dispersa.
- El usuario necesita respuestas con la fuente citada y sin invenciones.

## Prerequisites

- Fuentes de datos accesibles: documentos (PDF, Word, hojas), Notion, Drive, Confluence, CRM, emails.
- Un modelo de embeddings y un LLM (en la nube con contrato de no-entrenamiento, o modelo abierto on-premise).
- Una base de datos vectorial (pgvector sobre PostgreSQL recomendado hasta ~1M de vectores).
- Backend para la ingesta y la API de consulta.
- Conocimiento del RGPD y control de acceso. Ver `references/compliance.md`.

## Build Workflow

### 1. Diagnostico y alcance
- Definir el caso de uso prioritario y acotado (un departamento, un tipo de consulta) con un dolor claro.
- Identificar las fuentes de datos y quien debe poder consultar que (permisos).

### 2. Preparar los datos (lo mas importante)
- Definir las fuentes canonicas (la version buena de cada cosa) y descartar duplicados y caducados. Basura dentro, basura fuera. Ver `references/data-preparation.md`.

### 3. Construir la ingesta
- Trocear cada documento en fragmentos (chunking inteligente).
- Generar embeddings de cada fragmento y almacenarlos en la base vectorial. Ver `references/retrieval-and-grounding.md`.

### 4. Construir el retrieval y el grounding
- Convertir la pregunta en vector, recuperar los fragmentos mas relevantes, reordenar (reranking) y filtrar por permisos.
- El LLM redacta usando SOLO esos fragmentos y **cita la fuente**. Si la respuesta no esta, dice que no lo sabe. Ver `references/retrieval-and-grounding.md`.

### 5. Desplegar
- Elegir nube (proveedor con contrato de no-entrenamiento) u on-premise (modelo abierto, datos que no salen). Ver `references/deployment-and-eval.md`.
- Integrar donde el equipo ya trabaja (chat web, Slack/Teams, CRM).

### 6. Evaluar
- Construir un set de preguntas reales con respuestas correctas y evaluar precision, relevancia del retrieval y tasa de "no lo se". Iterar sobre las respuestas malas (casi siempre es retrieval o un documento sucio, no el modelo).

## Architecture (resumen)

```
FASE 1 (ingesta):  Fuentes -> Chunking -> Embeddings -> Base vectorial
FASE 2 (consulta): Pregunta -> vector -> recuperar fragmentos -> reranking + permisos
                   -> LLM redacta con esos fragmentos, citando la fuente
```

Detalle en `references/architecture.md`.

## Guardrails

- Grounding estricto: el modelo responde SOLO desde los fragmentos recuperados.
- Si no encuentra la informacion en los datos, dice que no la tiene; NO la inventa.
- Respetar permisos por documento (ACLs) en la recuperacion; nunca "un unico saco" sin control de acceso.
- Los proveedores no entrenan con los datos (por contrato); opcion on-premise para lo sensible.

## Resources

- `references/architecture.md` -- Fases de ingesta y consulta, componentes.
- `references/data-preparation.md` -- Fuentes, curacion y chunking.
- `references/retrieval-and-grounding.md` -- Embeddings, bases vectoriales (pgvector), reranking, grounding anti-alucinacion, ACLs.
- `references/deployment-and-eval.md` -- Nube vs on-premise, modelos y evaluacion.
- `references/compliance.md` -- RGPD, no-entrenamiento, control de acceso.

## Key Principles

1. No falta informacion: falta acceso a la que ya existe. RAG resuelve el acceso.
2. RAG, no fine-tuning: controla la alucinacion, permite datos frescos y cita la fuente.
3. La calidad esta en el retrieval y en la curacion de datos, no en el modelo que redacta.
4. Privacidad y control de acceso desde el diseno: es lo que hace que una empresa se atreva a conectar sus datos.
