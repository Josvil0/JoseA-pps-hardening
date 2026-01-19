# Práctica 3.1.1: Apache Hardening (CSP, HSTS, Autoindex)

**Nombre:** Jose Alonso Villanova
**Repositorio Docker Hub:** Josvil13/pps:pr3.1.1

## Explicación de las medidas aplicadas:
1. **Deshabilitar Autoindex:** Se ha usado `a2dismod autoindex` y `Options -Indexes` para evitar el listado de archivos.
2. **HSTS:** Implementada cabecera de seguridad para forzar HTTPS durante 2 años.
3. **CSP:** Configurada política de seguridad de contenido para mitigar ataques XSS.
4. **Ocultación de Versión:** Configurado `ServerTokens ProductOnly` para no dar pistas al atacante.
