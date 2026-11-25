# Resultados comprobados y límites

Corte de validación: **25/11/2026**. Implementación privada de referencia: `25562b2`. Las capturas de este caso corresponden a esa versión local, con documentos y solicitante ficticios.

## Qué se comprobó

| Prueba | Resultado observado | Qué permite afirmar |
|---|---|---|
| Suite del backend | 23 pruebas aprobadas | Los casos automatizados revisan contratos, citas, historial, abstención, propuestas, caducidad, duplicados y rollback |
| Compilación de interfaz | Correcta | El frontend genera su distribución local |
| Recorrido con servicios reales | 10 comprobaciones correctas | Conexión de servicios, corpus/PDF, saludo, cita literal, generación, abstención, ticket idempotente, HTTP y listado nativo autenticado de FreeITSM |
| Reinicio de contenedores | Conservó el ticket de prueba | Persistencia del volumen local |
| Capturas del portal | Respuesta con fuente y ticket de autorización de software | Funcionamiento visible de estos ejemplos, sin sustituir datos por imágenes simuladas |

La suite usa modelos simulados para comprobar comportamiento del código. El recorrido real usa Ollama y FreeITSM; no es una ronda completa de evaluación semántica. Los resultados completos y registros de consultas permanecen privados.

## Lo que muestra el recorrido

La pregunta sobre contraseñas recibió una respuesta con longitud mínima de 12 caracteres y los tipos exigidos por la política ficticia, con referencia a POL-002 p.1 §2.2. El panel de fuente muestra el fragmento original.

La petición de instalar software no aprobado remitió a POL-002 p.2 §2.5 y ofreció crear un ticket. Después de confirmarlo, el portal mostró el registro pendiente y la misma solicitud en el listado. El filtro «aplicación» muestra una fila de los dos tickets de laboratorio; el otro procede de una comprobación anterior fuera del corpus. No son métricas empresariales.

## Rendimiento observado

Una prueba inicial agotó 300 segundos con la configuración de memoria original. Se ajustó el contexto local a 8,192 tokens y la liberación del modelo de embeddings. La muestra posterior produjo una respuesta en 16.57 segundos y una abstención en 5.56 segundos. En el recorrido visual, otras ejecuciones mostraron 23.6 segundos para la respuesta y 10.6 para la solicitud de software.

Estos tiempos varían según carga, modelo, contexto y memoria. No son un benchmark ni un compromiso de servicio. El ajuste muestra que la operación necesita pruebas de capacidad, además de que los servicios estén conectados.

## Límites que permanecen

- No se certifica una precisión de 90% ni una tasa general de acierto. Las evaluaciones históricas detectaron errores de interpretación y escalamiento.
- Una referencia correcta no garantiza que toda la respuesta sea correcta; la revisión por el mismo LLM puede aceptar errores.
- La proporción de consultas sin propuesta de ticket no mide exactitud ni ahorro de soporte.
- Los PDF escaneados requieren OCR previo. El contexto y las conversaciones extensas tienen límites.
- La aplicación no implementa permisos por empleado o documento ni se presenta como servicio productivo.
- La integración SQL omite automatismos de FreeITSM; no se comprobaron envíos de correo o cálculo SLA.
- No se midieron ahorro económico, adopción, satisfacción ni reducción de carga de una empresa.

Para ampliar el caso propondría un piloto comparativo con revisión humana, preguntas separadas del corpus y medición de utilidad, errores, tiempos y costo total. Es una mejora propuesta, no un resultado conseguido.
