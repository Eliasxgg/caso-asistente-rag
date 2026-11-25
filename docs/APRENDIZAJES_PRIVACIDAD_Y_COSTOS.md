# Aprendizajes: RAG interno, privacidad y costos

## De consultar documentos a apoyar una tarea

Este proyecto me ayudó a comprender cómo podría funcionar un RAG dentro de una empresa: organizar documentos, buscar fragmentos relacionados con una pregunta y usarlos como contexto para generar una respuesta que se pueda revisar. En el prototipo el alcance fue pequeño, con cinco políticas ficticias y escalamiento a tickets. No fue una implantación empresarial.

El valor potencial está en facilitar consultas repetidas y mantener el vínculo con su fuente. No medimos una reducción real de tiempos de soporte ni reemplazamos el criterio de quien autoriza una solicitud.

## RAG, inferencia y entrenamiento

| Concepto | Qué significa aquí |
|---|---|
| Indexación | Extraer texto de los PDF, dividirlo y preparar su búsqueda |
| Embeddings | Representar textos como vectores para recuperar contenido relacionado |
| RAG | Recuperar fragmentos y entregarlos como contexto al modelo al responder |
| Inferencia local | Ejecutar los modelos preentrenados en el equipo mediante Ollama |
| Entrenamiento o fine-tuning | Modificar los pesos de un modelo; no se realizó en este proyecto |

Actualizar documentos y reconstruir el índice permite cambiar la información consultable sin entrenar de nuevo los modelos. Eso no hace que cualquier documento sea legible automáticamente: los PDF escaneados necesitan OCR previo y la recuperación puede seleccionar fragmentos insuficientes.

La [API de embeddings de Ollama](https://docs.ollama.com/api/embed) documenta la representación vectorial. El [trabajo original sobre RAG](https://arxiv.org/abs/2005.11401) es una referencia conceptual; este prototipo no reproduce su entrenamiento ni su arquitectura completa.

## Qué aporta ejecutar los modelos localmente

Comprendí que una organización puede tener más control sobre dónde procesa sus documentos y consultas si mantiene la inferencia en su infraestructura. En el flujo revisado del prototipo, el backend consulta modelos locales y no utiliza una API externa de generación. Las reglas y las consultas de demostración son ficticias.

Ese control requiere trabajo: permisos sobre documentos y respaldos, acceso de usuarios, retención de conversaciones, actualizaciones y protección de los servicios. El RAG no implementa permisos documentales distintos por empleado; antes de usar información interna real habría que incorporarlos. Las consultas y los embeddings también deben tratarse como información potencialmente sensible.

**Local no significa aislado de Internet ni seguro automáticamente.** La instalación y las actualizaciones pueden necesitar conexiones externas. Ollama ofrece funciones locales y de nube; habría que revisar y configurar las permitidas para cada organización. Su [FAQ oficial](https://docs.ollama.com/faq#does-ollama-send-my-prompts-and-answers-back-to-ollamacom) explica el tratamiento al ejecutar localmente y el modo sin funciones de nube. No realizamos una auditoría de tráfico ni certificamos ausencia total de comunicaciones externas.

Una solución gestionada en nube también puede ofrecer controles de privacidad; habría que evaluar su contrato, configuración y flujo concreto. La comparación no consiste en asumir que toda nube expone los datos o que cualquier servidor local los protege.

## ¿Cuándo podría convenir un RAG interno?

Aprendí a plantearlo como una decisión de negocio. No compraría equipo ni montaría infraestructura dedicada solo por incorporar IA. Primero definiría qué consultas se quieren resolver, con qué documentos y para cuántas personas.

| Opción a comparar | Cuándo merece evaluarse | Qué costo o límite revisar |
|---|---|---|
| Búsqueda documental o FAQ | Pocas preguntas y documentos fáciles de localizar | Mantenimiento del contenido y tiempo de búsqueda |
| RAG con modelos locales | Necesidad de control del procesamiento y consultas que justifican un piloto | Hardware, memoria, concurrencia, energía, operación y evaluación |
| RAG con modelos gestionados | Interesa reducir operación del modelo o disponer de otra capacidad | Consumo, contrato de datos, conectividad, integración y controles |

Esta tabla es un criterio de comparación, no una recomendación de compra basada en un estudio económico realizado. Un RAG tampoco exige un rack físico ni garantiza que haga falta un servidor propio: la infraestructura depende de la carga y los requisitos.

## Costos que incluiría en una evaluación

- **Iniciales:** preparación de documentos, integración, permisos, pruebas y equipo si el existente no alcanza.
- **Recurrentes:** energía, almacenamiento, respaldos, actualizaciones, soporte y tiempo de evaluación humana.
- **De capacidad:** usuarios simultáneos, memoria de los modelos y tiempos de respuesta aceptables.
- **De calidad:** correcciones, respuestas incorrectas y derivaciones innecesarias al soporte.

No tener una factura por cada consulta a una API no convierte la operación local en gratuita. Como marco de análisis usaría:

**Costo total del período = inversión atribuible al período + operación + mantenimiento + revisión de calidad.**

Para estimar un beneficio de tiempo, mediría consultas realmente resueltas, minutos ahorrados frente al método anterior y costo del tiempo involucrado. Compararía ese beneficio con el costo total, sin contar como ahorro todas las respuestas que genera el bot. Los errores y la revisión también consumen tiempo. No calculamos estos valores ni un retorno de inversión en el proyecto.

## Cómo lo justificaría mediante un piloto

1. Seleccionar un conjunto pequeño de documentos vigentes y preguntas reales autorizadas.
2. Comparar búsqueda/FAQ y RAG con los mismos casos.
3. Revisar respuestas, citas, abstenciones y escalamiento con una persona conocedora del tema.
4. Medir tiempos completos, capacidad simultánea y esfuerzo de mantenimiento.
5. Decidir continuar, reducir el alcance o mantener una alternativa más sencilla.

Mi conclusión de aprendizaje es que una solución pequeña puede servir para explorar una necesidad concreta. Su ampliación se debe justificar con evidencia de utilidad, calidad y costo; no por usar IA como fin en sí mismo.
