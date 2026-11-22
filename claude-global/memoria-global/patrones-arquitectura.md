# Patrones de arquitectura reutilizables

## Python — herramientas CLI + servidor MCP (de gemini-notebook-mcp-cli)
- **Capas estrictas:** `core/` (cliente HTTP de bajo nivel, sin lógica de negocio) → `services/` (toda la lógica y validación, devuelve dicts tipados) → `cli/` y `mcp/` como envoltorios finos. `cli/` y `mcp/` **nunca** importan de `core/`. Así CLI y MCP comparten comportamiento y tests.
- **Errores de servicio estructurados:** `ServiceError(message, user_message, hint, category, retryable, suggested_action, …)` con `.details()` para clientes máquina; subclases `ValidationError`, `NotFoundError`. Los servicios nunca dejan escapar excepciones crudas.
- **Reintentos:** backoff exponencial para 429/5xx (3 intentos, 1s→16s) y también para errores de "throttling" del propio protocolo (RPC code 8).
- **APIs internas no oficiales (IDs que rotan):** detectar deriva de forma ruidosa (`RPCDriftError` cuando la respuesta trae otro ID), registrar los IDs recibidos con `--debug`, y permitir *hot-patch* por variable de entorno JSON (`*_RPC_OVERRIDES`) sin publicar versión.
- **Auth por cookies:** guardar solo cookies; extraer CSRF/sesión/build-label automáticamente. Perfiles por cuenta en `~/.<app>/profiles/<name>/auth.json`. Auto-recuperación: recargar cookies más nuevas del disco o refresco headless del navegador; comando `auth refresh` para schedulers y opción de desactivarlo (cuentas Workspace).
- **Operaciones destructivas** exigen `confirm=True` en la herramienta MCP (borrar, sincronizar, generar).
- **Asistentes que escriben configs ajenas:** respaldo antes de cada cambio, fallar cerrado si el config está mal formado, preservar entradas no relacionadas, no tocar JSONC si no se puede editar con seguridad, reportar "omitido/fallido" con honestidad.
- **Rutas de almacenamiento sobreescribibles por env var** (`NOTEBOOKLM_MCP_CLI_PATH`) para que los tests no escriban en el home real.
- **Tests:** unitarios por servicio en `tests/services/`; marcadores pytest `e2e`, `integration`, `wizard_e2e` excluidos por defecto vía `addopts`; e2e del asistente interactivo con pexpect + pyte en un HOME aislado.

## Python — búsqueda local sin dependencias (de ui-ux-pro-max-skill)
- Motor BM25 implementado a mano + regex, configurado por un dict `CSV_CONFIG` por dominio (`file`, `search_cols`, `output_cols`); auto-detección de dominio si no se pasa `--domain`.
- Solo stdlib → funciona en cualquier máquina con Python 3; en Windows llamar `python` (el CLI usa un wrapper `run-python.mjs` multiplataforma).
- Validaciones de datos como scripts (`validate-csv`, `validate_data.py` semántico, evaluación de relevancia con splits calibración/held-out, smoke tests por dominio y stack).

## Node/TypeScript — CLI instalador de "skills" (de ui-ux-pro-max-skill)
- Fuente de verdad única (`src/…`) + script de sincronización que copia a los destinos empaquetados, con modo `--check` usado en CI.
- **No usar symlinks** en repos que se clonan en Windows: se vuelven archivos de texto y rompen el skill. Copiar archivos reales y verificar sincronía.
- Plantillas base + JSON por plataforma para generar el SKILL.md de cada asistente.
- `prepublishOnly` encadena sync → verificación de datos → typecheck → build.
- Rutas en skills relativas al propio SKILL.md (funcionan fuera del checkout).

## CI / releases (ambos)
- Versión única replicada en varios archivos → workflow que verifica que coincidan.
- Acciones de GitHub fijadas por SHA con comentario de versión.
- semantic-release con conventional commits (ui-ux) o CHANGELOG "Keep a Changelog" manual con créditos a contribuidores (gemini).
