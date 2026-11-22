---
name: aprender-proyecto
description: Analiza la sesión actual o proyectos anteriores para extraer patrones, arquitectura, decisiones técnicas y preferencias del usuario, guardándolos en la memoria persistente.
---

# Instrucciones de Aprendizaje y Memoria

Cuando el usuario ejecute `/aprender-proyecto` o te pida recordar lo aprendido:

1. **Revisión de contexto:** Analiza el historial de la sesión actual y los archivos clave del proyecto (`package.json`, `README.md`, estructura de carpetas o `CLAUDE.md` existente).
2. **Extracción de conocimiento:** Identifica y resume:
   - Stack tecnológico y convenciones de código usadas.
   - Errores resueltos y soluciones aplicadas (para no repetirlos).
   - Decisiones de arquitectura y reglas de negocio.
   - Preferencias explícitas del usuario (tono, formato, herramientas).
3. **Almacenamiento persistente:**
   - Actualiza el archivo `CLAUDE.md` en la raíz del proyecto con las reglas permanentes.
   - Guarda un resumen técnico en `~/.claude/memory/proyectos/[nombre-proyecto].md` para que esté disponible como referencia cruzada en futuros proyectos.
4. **Confirmación:** Muestra un breve listado con viñetas de los puntos nuevos que acabas de memorizar.
