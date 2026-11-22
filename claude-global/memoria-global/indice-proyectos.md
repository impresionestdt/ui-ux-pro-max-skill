# Índice de proyectos absorbidos

> Ambos repos son **forks** en `impresionestdt/`; el código lo escribieron
> sobre todo los mantenedores originales (no el usuario). Absorbido: 2026-11-22.

## ui-ux-pro-max-skill
- **Ruta local:** `/home/user/ui-ux-pro-max-skill` · remoto `impresionestdt/ui-ux-pro-max-skill`
- **Qué es:** skill de diseño UI/UX para asistentes de IA (Claude Code, Cursor, Windsurf…) con bases de datos CSV consultables + CLI instalador npm (`uipro`).
- **Stack:** Python 3 stdlib (motor de búsqueda BM25 + regex, sin dependencias) · TypeScript/Node 18+ con Bun para el CLI (`commander`, `prompts`, `ora`, `chalk`) · CSV como base de datos · semantic-release (conventional commits) · GitHub Actions.
- **Versión:** CLI 2.5.0.
- **Pistas clave:** `src/ui-ux-pro-max/` es la fuente de verdad; se espeja a `cli/assets/` y `.claude/skills/` con `npm run sync:assets`, verificado en CI (`check:assets`).

## gemini-notebook-mcp-cli
- **Ruta local:** `/home/user/gemini-notebook-mcp-cli` · remoto `impresionestdt/gemini-notebook-mcp-cli`
- **Qué es:** servidor MCP + CLI (`nlm`, `notebooklm-mcp`) para la API interna (batchexecute) de Gemini Notebook / NotebookLM.
- **Stack:** Python ≥3.11 · uv + hatchling · FastMCP · Typer + Rich + questionary · httpx · pydantic v2 · Chrome DevTools Protocol (websocket-client) para login · pytest (+asyncio, pexpect/pyte para e2e de TTY) · ruff + mypy strict.
- **Versión:** 0.13.0.
- **Pistas clave:** arquitectura en capas `core/ → services/ → cli/ + mcp/`; versión replicada en 5 archivos; CHANGELOG obligatorio por release.
