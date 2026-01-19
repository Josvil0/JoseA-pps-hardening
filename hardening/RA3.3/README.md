# RA3.3 - Apache Hardening

**Estudiante:** Jose Alonso  
**Imagen Docker Hub:** `josea13/pps:pr3.3`

## Implementación de Seguridad
Se han aplicado las siguientes directivas de fortalecimiento según la guía de Geekflare:
- **ServerTokens Prod & ServerSignature Off:** Eliminación de la versión del servidor en cabeceras y páginas de error.
- **Options -Indexes:** Desactivación del listado automático de archivos en directorios.
- **TraceEnable Off:** Protección contra ataques de Cross-Site Tracing (XST).
- **LimitExcept:** Restricción de métodos HTTP solo a GET, POST y HEAD.
- **Cabeceras de Seguridad:** Implementación de `X-Frame-Options`, `X-XSS-Protection` y `X-Content-Type-Options`.
- **Timeout:** Reducción a 60 segundos para prevenir ataques de denegación de servicio tipo Slowloris.

## Validación
- Comprobación de cabeceras mediante `curl -I`.
- Verificación de error 403 al intentar acceder a directorios sin index.
- Confirmación de bloqueo del método TRACE.
