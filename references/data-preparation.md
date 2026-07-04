# Preparacion de los datos

La calidad de las respuestas depende de la calidad de los datos. "Basura dentro, basura
fuera" se cumple aqui sin piedad. La curacion inicial vale mas que cualquier ajuste
posterior del modelo.

## Que fuentes conectar
- Documentos: PDFs, Word, hojas de calculo, presentaciones.
- Herramientas: Notion, Google Drive, Confluence, SharePoint, el CRM.
- Comunicacion: emails y, si aplica, historicos de tickets.
- Bases de datos y paginas web internas.

## Curar antes de ingerir
- Definir las **fuentes canonicas**: la version buena de cada cosa.
- Eliminar duplicados y versiones viejas. Un documento obsoleto en el sistema es peor
  que no tenerlo: genera respuestas equivocadas con aire de certeza.
- Estructurar lo que este suelto.

## Chunking (troceado)
- Fragmentos ni tan cortos que pierdan contexto ni tan largos que metan ruido.
- Respetar la estructura del documento (secciones, encabezados) al trocear.
- Usar solape entre fragmentos para no cortar ideas a la mitad.
- Guardar con cada fragmento su metadato de origen (documento, seccion, permisos) para
  poder citar la fuente y filtrar por acceso despues.

## Regla
Antes de ingerir, hacer limpieza. La curacion de datos es la palanca de calidad numero
uno de todo el sistema.
