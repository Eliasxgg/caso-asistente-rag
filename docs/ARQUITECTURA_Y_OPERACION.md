# Arquitectura y operación

## Componentes del laboratorio

| Componente | Función | Dónde se ejecuta |
|---|---|---|
| React y Vite | Chat, fuentes PDF, biblioteca y consulta de tickets | Equipo local |
| Python y FastAPI | Recuperación, generación, citas y confirmación de solicitudes | Equipo local |
| pypdf | Extracción del texto de los documentos | Backend |
| BM25 y BGE-M3 | Recuperación léxica y semántica, combinada por fusión de rankings | Backend y Ollama local |
| Qwen2.5:7b | Respuesta y revisión mediante un modelo preentrenado | Ollama local |
| SQLite y caché de vectores | Propuestas, registro de consultas y reutilización de embeddings | Almacenamiento local privado |
| MySQL 8.0.45 | Persistencia de solicitantes, tickets y mensajes | Contenedor propio |
| FreeITSM 5.11.0 | Aplicación de mesa de ayuda y esquema oficial | Contenedor propio |

Los documentos son cinco políticas ficticias de jornada, seguridad de la información, teletrabajo, inventario/despacho y atención/devoluciones. Su índice tiene 60 fragmentos en la versión comprobada. No se usa una base de datos empresarial real ni se entrenó un modelo propio.

## Respuesta y respaldo

La recuperación selecciona contenido antes de generar la respuesta. El servidor construye los metadatos de las citas y permite abrir el fragmento y su PDF. Otra llamada al modelo revisa la respuesta; esa verificación también puede equivocarse. Si la búsqueda semántica falla, el código puede utilizar búsqueda léxica, con menor capacidad para relacionar formulaciones.

El sistema detecta cambios en los PDF y reconstruye el índice. No incluye OCR automático ni una gestión empresarial completa de versiones, permisos o aprobación de documentos.

## Integración de tickets

La consulta prepara una propuesta; la persona confirma su registro. El backend utiliza SQL fijo y parametrizado, una transacción y un número estable para la propuesta. Repetir su confirmación reutiliza el ticket. El solicitante no se asigna automáticamente como propietario del trabajo.

La integración escribe en la base real de FreeITSM y el portal consulta sus tickets. **La escritura directa no ejecuta los hooks, notificaciones, auditorías de aplicación ni cálculo automático SLA de FreeITSM.** Para un uso empresarial habría que evaluar su API oficial y el flujo completo de negocio. Crear el ticket tampoco implica que la solicitud haya sido aprobada.

## Local y nube

La versión presentada funciona localmente. Los servicios publicados escuchan solo en el equipo; el planificador de FreeITSM está desactivado y no se configuró entrega de correo externo. No hay una demo pública de esta aplicación ni despliegue VPS validado.

Una posible instalación interna necesitaría autenticación, permisos por documento, TLS, gestión de secretos, respaldos y evaluación de capacidad. La ubicación de los modelos también requiere decidirse; no se presupone que una VPS pequeña pueda ejecutar esta carga ni que todos los componentes deban ir en una sola máquina.
