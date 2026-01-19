# RA3.1.2 - WAF ModSecurity

**Estudiante:** Jose Alonso 
**Imagen Docker Hub:** `josea13/pps:pps_pr3.1.2`

## Implementación de Seguridad
Se ha implementado un Firewall de Aplicación Web (WAF) utilizando ModSecurity para proteger el servidor contra ataques de capa 7:
- **ModSecurity Engine:** Configurado en modo `On` para detectar y bloquear ataques en tiempo real (sustituyendo el modo por defecto `DetectionOnly`).
- **OWASP Core Rule Set (CRS):** Integración de las reglas estándar de la industria para mitigar las vulnerabilidades del "Top 10 de OWASP".
- **Protección contra Inyección:** Reglas activas para identificar y denegar intentos de SQL Injection y Command Injection.
- **Prevención de XSS:** Filtrado de etiquetas `<script>` y otros vectores de Cross-Site Scripting en parámetros GET y POST.
- **Protocol Anomaly Detection:** Bloqueo de peticiones mal formadas que no cumplen con los estándares HTTP.

## Validación
- **Simulación de Ataque SQLi:** Intento de acceso mediante parámetros maliciosos como `' OR 1=1 --`, resultando en error **403 Forbidden**.
- **Simulación de Ataque XSS:** Inyección de código JavaScript `<script>` en la URL, verificando el bloqueo automático por el WAF.
- **Inspección de Logs:** Verificación en el log de auditoría de ModSecurity de los intentos de intrusión registrados y bloqueados.
