---
name: absorber-proyectos
description: Escanea proyectos realizados anteriormente para extraer arquitectura, patrones de código, convenciones y lecciones aprendidas, guardándolos en la memoria global de Claude. Úsala cuando el usuario pida aprender de un proyecto pasado o consultar conocimiento previo.
---

# Absorbedor de Conocimiento de Proyectos

## Objetivo
Extraer conocimiento reutilizable de proyectos terminados y mantener una base de memoria global en `~/.claude/memoria-global/` para aplicarla en futuros desarrollos.

## Proceso de Absorción (Cuando se apunta a un proyecto)
1. **Exploración inicial:** Lee el `README.md`, archivos de configuración (`package.json`, `pyproject.toml`, `docker-compose.yml`, etc.) y la estructura de carpetas del proyecto indicado.
2. **Extracción de conocimiento:** Identifica y resume:
   - **Stack y versiones:** Librerías principales y herramientas usadas.
   - **Arquitectura y patrones:** Estructura de carpetas, manejo de estado, conexión a bases de datos y autenticación.
   - **Convenciones y estilo:** Reglas de formato, nombrado y estructura de pruebas.
   - **Soluciones clave (Gotchas):** Problemas complejos resueltos o configuraciones críticas que evitaron errores.
3. **Almacenamiento:** Guarda o actualiza los siguientes archivos en `~/.claude/memoria-global/`:
   - `indice-proyectos.md`: Resumen de cada proyecto absorbido, su stack y ruta local.
   - `patrones-arquitectura.md`: Soluciones reutilizables clasificadas por tecnología.
   - `preferencias-usuario.md`: Estándares personales detectados en el código.
4. **Deduplicación:** Antes de escribir, lee los archivos existentes en `~/.claude/memoria-global/` para evitar duplicar reglas y consolidar mejoras.

## Proceso de Recuperación (Al iniciar o trabajar en un proyecto nuevo)
1. Consulta `indice-proyectos.md` y `patrones-arquitectura.md` antes de proponer una arquitectura nueva.
2. Si el proyecto actual comparte tecnologías con uno anterior, aplica las mismas convenciones y alerta al usuario si se repite un patrón que ya dio problemas en el pasado.
