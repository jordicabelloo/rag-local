# Retrieval y grounding

Recuperar bien es lo que separa un RAG util de uno que responde regular. La generacion
es la parte facil; la recuperacion es donde se gana la precision.

## Embeddings
Un embedding es un vector que representa el significado de un fragmento de texto. Dos
textos que hablan de lo mismo tienen vectores cercanos, aunque usen palabras distintas.
Asi el sistema encuentra la respuesta aunque el usuario no use las palabras del
documento (busqueda por significado, no por palabras exactas).

## Base de datos vectorial

| Opcion | Cuando encaja |
|--------|---------------|
| pgvector (PostgreSQL) | Ya usas Postgres; hasta ~1M de vectores; transacciones ACID |
| Base vectorial dedicada | Gran volumen o busqueda muy exigente |
| On-premise | Los datos no pueden salir de tu infraestructura |

## Recuperar los fragmentos correctos
- **Chunking inteligente**: ver `data-preparation.md`.
- **Reranking**: reordenar los candidatos para quedarte con los mas relevantes.
- **Filtrado por permisos**: recuperar solo lo que el usuario puede ver (ACLs).
- **Ventana de contexto controlada**: pasar al modelo lo justo, no todo.

## Grounding estricto (anti-alucinacion)
- El modelo redacta usando SOLO los fragmentos recuperados.
- Si la respuesta no esta ahi, NO la inventa: dice que no la tiene y sugiere a quien
  consultar. Una respuesta "no lo se" vale mil veces mas que una inventada con seguridad.
- Tecnicas: grounding estricto, ventanas de contexto acotadas y RAG reflexivo
  (Self-RAG), que hace que el sistema decida cuando necesita buscar mas antes de responder.
- Citar siempre el documento (y pagina/seccion) de donde sale la respuesta: da
  confianza y obliga a responder desde datos.

## El error mas caro
Un RAG que recupera mal responde con seguridad usando el fragmento equivocado. El
trabajo fino no esta en el modelo que redacta, sino en recuperar el contexto correcto.
