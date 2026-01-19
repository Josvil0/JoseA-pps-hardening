# RA3.1 - Práctica 4: Evitar ataques DoS

**Estudiante:** Jose Alonso
**Imagen Docker Hub:** `josea13/pps:pr4`

## Descripción
Se ha incorporado el módulo **mod_evasive** para proteger el servidor Apache contra ataques de Denegación de Servicio (DoS). El módulo detecta ráfagas de peticiones desde una misma IP y las bloquea temporalmente.

## Implementación
1. **Heredabilidad:** `FROM josea13/pps:pr3.1.3` (mantiene WAF y OWASP).
2. **Instalación:** Módulo `libapache2-mod-evasive`.
3. **Configuración:**
   - `DOSPageCount 2`: Bloquea si se pide la misma página > 2 veces/seg.
   - `DOSBlockingPeriod 10`: Baneo de 10 segundos tras detectar el ataque.
   - Directorio de logs: `/var/log/mod_evasive`.

## Validación con Apache Bench (ab)
Se ha realizado un ataque de 100 peticiones con una concurrencia de 10:
`ab -n 100 -c 10 http://localhost:8083/index.html`

**Resultado del informe:**
- **Complete requests:** 100
- **Non-2xx responses:** 82
- **Conclusión:** El sistema ha bloqueado exitosamente 82 peticiones mediante un error **403 Forbidden**, demostrando que el escudo contra DoS está activo.
