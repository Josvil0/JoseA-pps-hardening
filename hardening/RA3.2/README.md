# RA3.2 - Certificado Digital en Apache

**Estudiante:** Jose Alonso 
**Imagen Docker Hub:** `josea13/pps:pr3.2` 
**Dominio configurado:** `www.caminas.com`

## Descripción
Se ha configurado un servidor Apache bajo Debian con soporte SSL/TLS completo, utilizando un certificado auto-firmado generado mediante OpenSSL.

## Implementación
- **Certificado:** Generado con `CN=www.caminas.com`, ubicación `Castellón`.

## Validación
- Acceso exitoso desde la máquina host mediante el dominio `www.caminas.com`.
- Verificación de la redirección automática de HTTP a HTTPS.
- Inspección del certificado en el navegador confirmando los datos
