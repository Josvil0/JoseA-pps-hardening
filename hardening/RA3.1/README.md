# RA3.1 - Seguridad Progresiva y WAF

Este bloque implementa una estrategia de seguridad incremental en el servidor web, donde cada contenedor se construye utilizando como base la imagen de la práctica anterior.

## Estrategia de Capas (Cascada)
Para cumplir con los requisitos del proyecto, el despliegue sigue este orden de herencia:
`pr3.1.1` ➔ `pr3.1.2` ➔ `pr3.1.3` ➔ `pr3.1.4` ➔ `pr3.1.5`



## Estructura de las Prácticas y Pulls
| Práctica | Enfoque | Imagen Docker Hub (Pull) |
| :--- | :--- | :--- |
| **[3.1.1](./RA3_1_1)** | Base Apache (CSP/HSTS) | `docker pull josea13/pps:pr3.1.1` |
| **[3.1.2](./RA3_1_2)** | Migración Nginx | `docker pull josea13/pps:pr3.1.2` |
| **[3.1.3](./RA3_1_3)** | Integración PHP Hardening | `docker pull josea13/pps:pr3.1.3` |
| **[3.1.4](./RA3_1_4)** | ModSecurity (Detection) | `docker pull josea13/pps:pr3.1.4` |
| **[3.1.5](./RA3_1_5)** | WAF Full Blocking Mode | `docker pull josea13/pps:pr3.1.5` |

##  Despliegue rápido (WAF final)
La imagen final `pr3.1.5` acumula todas las capas de seguridad anteriores:
```bash
docker run -d -p 443:8443 -e DETECTION_ONLY=0 josea13/pps:pr3.1.5
```

