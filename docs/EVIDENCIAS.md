# Evidencias del recorrido

Las seis imágenes se capturaron en el navegador sobre el laboratorio local el **25/11/2026**. Son pantallas reales de la aplicación; no son composiciones, mockups ni una demostración cloud. La empresa, las reglas y el solicitante son ficticios.

| Imagen | Qué muestra | Cómo interpretarla |
|---|---|---|
| [01 · Inicio](capturas/01-inicio.jpg) | Portal y aviso académico | Entrada a la demo, sin acreditar autenticación empresarial |
| [02 · Respuesta](capturas/02-respuesta-con-fuente.jpg) | Consulta sobre reglas de contraseña y referencia POL-002 p.1 §2.2 | Ejemplo generado por Ollama con contexto; no una medición de exactitud global |
| [03 · Biblioteca](capturas/03-biblioteca.jpg) | Catálogo con cinco documentos; tres tarjetas visibles | Políticas de laboratorio consultables |
| [04 · Fuente](capturas/04-detalle-fuente.jpg) | Texto original, archivo, sección y página | Permite contrastar la respuesta con el fragmento |
| [05 · Confirmación](capturas/05-ticket-confirmado.jpg) | Registro de una solicitud de autorización de software | Confirmación de ticket, sin aprobar la instalación |
| [06 · Tickets](capturas/06-listado-tickets.jpg) | Consulta de FreeITSM desde el portal RAG, filtrada por «aplicación» | Una solicitud de dos tickets ficticios; no es la interfaz administrativa nativa de FreeITSM |

En la prueba técnica previa se comprobó también el ticket por la API nativa autenticada de FreeITSM y su persistencia tras reiniciar contenedores. No se utiliza una captura aislada de una herramienta para simular una integración dentro del portal.

Los registros completos, credenciales y archivos de entorno permanecen fuera de este repositorio. Los números de ticket visibles pertenecen exclusivamente al laboratorio.
