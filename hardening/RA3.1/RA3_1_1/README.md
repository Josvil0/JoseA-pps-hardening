# Hardening de Servidor Web Apache (RA3.1.1)

**Autor:** Jose Alonso Villanova

**Imagen Docker Hub:** Josea13/pps:pr3.1.1

```markdown
**Comando para descargar la imagen:**
`docker pull josea13/pps:pr3.1.1`
```
## Introducción  

Este proyecto implementa un despliegue securizado de Apache sobre Ubuntu 22.04. Se han aplicado directivas de endurecimiento basadas en las guías de OWASP para mitigar vectores de ataque como la exposición de información, el secuestro de sesiones y la inyección de scripts (XSS).  

## Medidas de Seguridad Implementadas

- **Desactivación de Autoindex:** Se ha inhabilitado el módulo de listado de directorios para evitar la enumeración de archivos del servidor.
- **Implementación de HSTS:** Configuración de la cabecera Strict-Transport-Security para garantizar que todas las comunicaciones se realicen exclusivamente a través de HTTPS.
- **Configuración de CSP (Content Security Policy):** Establecimiento de una política de seguridad que restringe los orígenes permitidos para la carga de recursos, bloqueando la ejecución de scripts no autorizados.
- **Cifrado SSL/TLS:** Configuración de certificados digitales para proteger la integridad y confidencialidad de los datos en tránsito.

## Infraestructura y Despliegue

Para garantizar un entorno aislado y reproducible, se utiliza Docker mapeando los puertos de servicio estándar (80 y 443) a puertos locales.

```bash
docker run -d --name pps3.1.1 -p 8080:80 -p 8081:443 josea13/pps:pr3.1.1  
  
```

![Foto 1 - Contenedor en ejecucion](img/foto1.png)


## Verificación de Medidas (Evidencias)

### Análisis de Cabeceras de Seguridad

Validación de la correcta entrega de las directivas HSTS y CSP mediante una petición de encabezados.  

```bash
curl -kI https://localhost:8081
```

![Foto 2 - Cabeceras de seguridad](img/foto2.png)

###  Restricción de Acceso a Directorios

Verificación de que el servidor no permite listar el contenido de carpetas que carecen de un archivo de índice.
```bash
curl -I https://localhost:8080/test/  
```
 
![Foto 3 - Sin acceso a directorios](img/foto3.png)

### Validación del Protocolo Seguro (SSL/TLS)

Acceso al servicio mediante el puerto seguro para verificar la correcta carga del sitio bajo HTTPS.

![Foto 4 - Interfaz web](img/foto4.png)

##  Conclusiones

Estas medidas permiten reducir la superficie de ataque del servidor y evitar configuraciones inseguras por defecto.
