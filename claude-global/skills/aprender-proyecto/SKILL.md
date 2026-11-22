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
   - Guarda la memoria entre proyectos en `~/.claude/memoria-global/` (la misma que usa `absorber-proyectos`). Antes de escribir, lee los archivos existentes para no duplicar y consolida lo que ya esté:
     - `indice-proyectos.md`: añade o actualiza la entrada del proyecto (stack, ruta local, enlace a su resumen).
     - `proyectos/[nombre-proyecto].md`: resumen técnico detallado del proyecto (decisiones, errores resueltos, reglas de negocio).
     - `patrones-arquitectura.md`: soluciones reutilizables, clasificadas por tecnología.
     - `preferencias-usuario.md`: preferencias explícitas del usuario.
4. **Confirmación:** Muestra un breve listado con viñetas de los puntos nuevos que acabas de memorizar.
