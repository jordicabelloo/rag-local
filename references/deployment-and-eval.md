# Despliegue y evaluacion

## Nube u on-premise

Decision de privacidad y coste. El camino correcto depende de la sensibilidad de los datos.

| | Nube (proveedor enterprise) | On-premise / modelo abierto |
|--|------------------------------|------------------------------|
| Privacidad | Alta, con contrato de no-entrenamiento | Maxima, los datos no salen |
| Calidad | Modelos punteros | Muy buena con modelos abiertos |
| Coste | Por uso | Infra propia, mas control |
| Cuando | La mayoria de casos | Datos muy sensibles o regulados |

Muchas empresas empiezan en la nube con un proveedor que garantiza por contrato no
entrenar con sus datos, y reservan el on-premise para lo mas sensible. Se puede
combinar: lo sensible en local, el resto en la nube.

## Integraciones
- Entrada de datos: Drive, Notion, Confluence, SharePoint, CRM, helpdesk, email.
- Salida (donde se pregunta): chat web interno, Slack/Teams, widget de soporte.
- Cuanto mas cerca este de donde la gente ya trabaja, mas se usa.

## Evaluacion (no solo lanzar)

| Metrica | Que mide |
|---------|----------|
| Precision de la respuesta | % de respuestas correctas y ancladas en fuente |
| Relevancia del retrieval | Si recupera los fragmentos correctos |
| Tasa de "no lo se" | Que reconozca cuando no tiene el dato (bueno) |
| Adopcion | Cuanta gente lo usa de verdad y con que frecuencia |
| Coste por consulta | Para controlar el gasto a escala |

Construir un set de preguntas reales con sus respuestas correctas y evaluar el sistema
contra el cada vez que se cambie algo. Revisar las respuestas malas: casi siempre el
fallo esta en el retrieval o en un documento sucio, no en el modelo. La precision y la
tasa de "no lo se" bien calibradas son lo que genera confianza.
