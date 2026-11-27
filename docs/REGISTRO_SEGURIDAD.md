# Registro de seguridad · Sistema Alumnos

Estudiante: Maximiliano Páez   Repositorio: ____________________   Fecha: 27/11/2026

Completa este registro a medida que avanzas. Cada fila debe poder seguirse hasta un **build de Jenkins**
y un **commit** (usa el identificador `VULN-xx` en el mensaje del commit).

## 1. Revisiones de seguridad realizadas

| # | Etapa del SDLC | Herramienta / técnica | Build | Resultado (resumen) |
|---|---|---|---|---|
| R1 | Código (SAST) | Bandit en el pipeline | #__ | 2 hallazgos High / 2 Medium / 1 Low (0 tras corrección) |
| R2 | Dependencias (SCA) | pip-audit en el pipeline | #__ | __ vulnerabilidades en __ paquetes |
| R3 | Pruebas dinámicas (DAST) | OWASP ZAP sobre staging | #__ | __ High / __ Medium / __ Low |
| R4 | Revisión manual | Lectura de `app.py` | — | 3 hallazgos: XSS reflejado, exposición de errores SQL y falta de cabeceras HTTP |
| R5 | Producción | Grafana + Prometheus | — | |

## 2. Vulnerabilidades identificadas y corregidas

| ID | Vulnerabilidad (CWE) | Detectada por | Ubicación | Riesgo | Corrección aplicada | Commit | Build que lo verifica |
|---|---|---|---|---|---|---|---|
| VULN-01 | Uso de hash débil MD5 (CWE-327) | Bandit (B324) | `app.py:221` | Alto | Reemplazo por `generate_password_hash` y `check_password_hash` de Werkzeug | `pendiente` | #__ |
| VULN-02 | Modo Debug activado (CWE-94) | Bandit (B201) | `app.py:241` | Alto | Desactivado con `debug=False` | `pendiente` | #__ |
| VULN-03 | Inyección SQL (CWE-89) | Bandit (B608) | `app.py:205` | Medio | Consulta parametrizada con `?` en `sqlite3` | `pendiente` | #__ |
| VULN-04 | Exposición en todas las interfaces (CWE-605) | Bandit (B104) | `app.py:241` | Medio | Uso de variable `FLASK_HOST` con valor por defecto `127.0.0.1` | `pendiente` | #__ |
| VULN-05 | Secreto hardcodeado (CWE-259) | Bandit (B105) | `app.py:20` | Bajo | Lectura de `SECRET_KEY` y credenciales desde variables de entorno | `pendiente` | #__ |
| VULN-06 | XSS Reflejado (CWE-79) | Revisión manual | `app.py:159` | Alto | Sanitización del parámetro `name` con `markupsafe.escape()` | `pendiente` | #__ |
| VULN-07 | Exposición de errores SQL (CWE-209) | Revisión manual | `app.py:209` | Medio | Registro solo en log interno y respuesta genérica HTTP 500 | `pendiente` | #__ |
| VULN-08 | Falta de cabeceras de seguridad HTTP | Revisión manual | `app.py:130` | Medio | Agregadas `X-Content-Type-Options`, `X-Frame-Options`, `CSP` y `Referrer-Policy` | `pendiente` | #__ |

## 3. Resultados de OWASP ZAP

| Alerta de ZAP | Riesgo | URL de ejemplo | VULN relacionada | Cómo se mitiga | ¿Mitigada? Build |
|---|---|---|---|---|---|
| | | | | | |

## 4. Monitoreo e incidentes

| Hora | Panel / métrica de Grafana | Qué se observó | Entorno | Clasificación | Acción de respuesta | Verificación |
|---|---|---|---|---|---|---|
| | | | | | | |

## 5. Gestión de dependencias

| Paquete | Versión inicial | Vulnerabilidades (IDs) | Versión final | Origen del cambio (PR de Dependabot / manual) | ¿Pruebas, pip-audit y ZAP siguen OK? Build |
|---|---|---|---|---|---|
| Flask | 2.2.2 | | | | |
| Werkzeug | 2.2.2 | | | | |
| Jinja2 | 3.1.2 | | | | |
| gunicorn | 21.2.0 | | | | |
| prometheus-client | 0.17.1 | | | | |

## 6. Trazabilidad

Pega aquí (o adjunta) el `TRAZABILIDAD.md` del último build y completa un recorrido por cada actividad del pipeline:

| Actividad | Hallazgo | Build que lo detectó | Commit / PR que lo resolvió | Build que lo verificó | Versión en producción |
|---|---|---|---|---|---|
| Revisión de seguridad (Bandit) | | #__ | | #__ | |
| Prueba automatizada (OWASP ZAP) | | #__ | | #__ | |
| Gestión de dependencias (Dependabot) | | #__ | PR #__ | #__ | |
