# Arquitectura RAG de principio a fin

Un sistema RAG tiene dos fases: preparar el conocimiento (una vez, y al actualizar) y
responder (en cada pregunta).

## Fase 1: ingesta del conocimiento

1. **Conectar fuentes**: recoger los documentos de todas las herramientas.
2. **Trocear (chunking)**: dividir cada documento en fragmentos manejables.
3. **Generar embeddings**: convertir cada fragmento en un vector (su significado).
4. **Almacenar**: guardar los vectores en una base de datos vectorial privada.

## Fase 2: responder una pregunta

1. La pregunta del usuario se convierte tambien en un vector.
2. Se recuperan los fragmentos mas parecidos (los mas relevantes).
3. Se ordenan por relevancia (reranking) y se filtran por permisos.
4. El LLM redacta la respuesta usando SOLO esos fragmentos, citando la fuente.

El usuario solo ve un chat donde pregunta. Debajo, todo esto ocurre en milisegundos.

## Componentes y stack

| Pieza | Opcion recomendada |
|-------|--------------------|
| Ingesta | Backend Python (loaders por tipo de fuente) |
| Chunking | Fragmentacion por semantica/estructura, con solape |
| Embeddings | Modelo de embeddings (nube o local) |
| Base vectorial | pgvector sobre PostgreSQL (hasta ~1M vectores) |
| Retrieval | Busqueda por similitud + reranking + filtro de permisos |
| Generacion | LLM con grounding estricto |
| Interfaz | Chat web, Slack/Teams, widget o API |

## Escala
Para la mayoria de empresas, pgvector es el punto dulce (reusas Postgres, guardas los
vectores junto a los datos, control total). Migrar a una base vectorial dedicada solo
cuando el volumen o la exigencia de busqueda lo pidan.
