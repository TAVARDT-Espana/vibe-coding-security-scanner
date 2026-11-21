# Vibe Coding Security Scanner y Auditor de Aplicaciones Generadas por IA | TAVARDT España

[![Español (España) Online Scanner](https://img.shields.io/badge/Esc%C3%A1ner%20Online-Probar%20Aplicaci%C3%B3n-1e00ff.svg?style=for-the-badge)](https://tavardt-espana.github.io/vibe-coding-security-scanner/)

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Vibe Coding Security](https://img.shields.io/badge/Vibe%20Coding-Security%20Hardened-00d26a.svg)](README.md)
[![Language](https://img.shields.io/badge/Language-Español%20(España)-green.svg)](README.md)
[![Engineering](https://img.shields.io/badge/TAVARDT-Cybersecurity-5b3cf5.svg)](https://ag.tavardt.com/es/ciberseguridad/)

Escáner open source para auditar aplicaciones creadas mediante vibe coding (Cursor, Lovable, Bolt, v0). Detecta claves API expuestas en frontend, brechas de RLS en Supabase y sourcemaps públicos.

Desarrollado y mantenido por el equipo de ingeniería de ciberseguridad de **[TAVARDT España](https://ag.tavardt.com/es/ciberseguridad/)**.

---

## 1. Visión General del Escáner de Seguridad Vibe Coding

El auge del desarrollo acelerado con inteligencia artificial (*vibe coding*) permite construir y publicar aplicaciones en minutos mediante **Cursor, Lovable.dev, Bolt.new, v0 y Replit**.

Sin embargo, la falta de revisión arquitectónica expone con frecuencia secretos de producción, bases de datos abiertas a cualquier usuario y código fuente sin compilar.

Este repositorio proporciona un escáner en Python para auditar **el perímetro público de cualquier aplicación web en producción**, detectando riesgos críticos de forma determinista.

---

## 2. Vulnerabilidades y Vectores Auditados

| Vector de Riesgo | Causa en Vibe Coding | Impacto Técnico |
| :--- | :--- | :--- |
| **Claves API en Frontend** | Desarrolladores ubican claves privadas de OpenAI (`sk-...`), Stripe o AWS en el `.env` del cliente. | Cualquier visitante extrae la clave desde DevTools y consume su saldo contratado. |
| **Supabase RLS Desactivado** | Se crean tablas en Supabase sin habilitar *Row Level Security* (RLS). | La `anon_key` pública permite consultar o vaciar tablas completas vía REST. |
| **Sourcemaps en Producción** | El compilador publica archivos `.js.map` en el hosting web. | El código fuente original completo queda expuesto para descarga pública. |
| **Archivos Sensibles Abiertos** | Configuraciones erróneas dejan rutas como `/.env` o `/.git/HEAD` públicas. | Filtración total de variables de entorno y secretos de infraestructura. |
| **Falta de Cabeceras Seguras** | Ausencia de directivas CSP, HSTS y X-Frame-Options. | Vulnerabilidad ante Clickjacking e inyecciones de código malicioso. |

---

## 3. Guía de Instalación y Ejecución

### Instalación Rápida

```bash
git clone https://github.com/TAVARDT-Espana/vibe-coding-security-scanner.git
cd vibe-coding-security-scanner
```

### Ejecutar Escaneo en una URL

```bash
python scanner.py https://su-aplicacion.vercel.app
```

### Parámetros Disponibles

```bash
# Salida en formato JSON estructurado
python scanner.py https://su-aplicacion.vercel.app --json

# Omitir análisis de sourcemaps
python scanner.py https://su-aplicacion.vercel.app --no-sourcemaps
```

---

## 4. Blindaje Profesional y Soporte Técnico

Si su diagnóstico reveló credenciales expuestas, tablas sin RLS en Supabase/Firebase o requiere blindaje perimetral:

* **Portal Corporativo:** [TAVARDT España](https://ag.tavardt.com/es/ciberseguridad/)
* **Contacto Técnico Directo:** [Contactar con el Equipo de Ingeniería](https://ag.tavardt.com/es/contacto/)

---

## Licencia

Distribuido bajo licencia de código abierto MIT. Consulte el archivo [`LICENSE`](LICENSE) para más detalles.  
Copyright (c) 2026 TAVARDT España.
