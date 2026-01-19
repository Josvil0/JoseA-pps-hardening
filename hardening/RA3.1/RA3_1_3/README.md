RA3.1 - Práctica 3.1.3: WAF con Reglas OWASP CRS

**Estudiante:** Jose Alonso
**Imagen Docker Hub:** `josea13/pps:pr3.1.3`

## Descripción
Se ha potenciado el WAF integrando el **Core Rule Set (CRS) de OWASP**, un conjunto de reglas profesionales que protegen contra inyecciones SQL, Path Traversal y ejecución de comandos (RCE).

## Implementación
1. **Heredabilidad:** `FROM josea13/pps:pr3.1.2`.
2. **OWASP CRS:** Clonación del repositorio oficial y carga de las reglas en `/etc/modsecurity/rules/`.
3. **Optimización:** Limpieza de la jerarquía de Apache para evitar IDs duplicadas y asegurar la protección en el puerto 80 y 443 (SSL).

## Validación del WAF (Reglas OWASP)
Se han realizado pruebas de penetración para confirmar que las reglas profesionales bloquean ataques complejos:

### Prueba 1: Ataque de Inyección de Comandos (RCE)
`curl -I "http://localhost:8083/index.html?exec=/bin/bash"`
**Resultado esperado:** `403 Forbidden`
