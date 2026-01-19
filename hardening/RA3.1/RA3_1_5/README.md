# RA3.1 - Práctica 5: Nginx con ModSecurity y OWASP CRS

**Estudiante:** Jose Alonso
**Imagen Docker Hub:** `josea13/pps:pr5`

## Descripción
Migración de las políticas de seguridad de Apache a **Nginx**. Se ha utilizado la imagen oficial de OWASP ModSecurity para garantizar la compatibilidad del conector ModSecurity-Nginx y el Core Rule Set (CRS).

## Implementación
1. **Imagen Base:** `owasp/modsecurity-crs:nginx`.


### Prueba:
`curl -I "http://localhost:8085/index.html?exec=/bin/bash"`
**Resultado esperado:** `403 Forbidden`
