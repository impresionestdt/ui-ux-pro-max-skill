# Preferencias y estándares del usuario

> Aviso: los dos proyectos absorbidos son forks; las convenciones de abajo son
> de los mantenedores originales, adoptadas por el usuario al trabajar en ellos.
> Confirmar con el usuario antes de tratarlas como preferencias personales.

## Flujo de trabajo
- Nunca empujar a `main`; trabajar en ramas `feat/…` o `fix/…` y abrir PR.
- Mensajes de commit **Conventional Commits** con scope: `feat(setup): …`, `fix(brand): …`, `docs: …`, `chore: prepare X.Y.Z release`.
- Mantener un `CLAUDE.md` (y `AGENTS.md`/`GEMINI.md`) detallado en la raíz con comandos, arquitectura y reglas.

## Python
- ruff (line-length 100, reglas E,F,I,UP,B,SIM; E501 ignorado) + `ruff format`; mypy strict.
- Tipado moderno (`str | None`, `collections.abc`), docstrings breves por módulo.
- uv para dependencias; rangos con cota superior (`>=x,<y`).

## Documentación
- CHANGELOG con secciones Added / Improved / Fixed / Verification, redactado para usuarios finales.
- READMEs multilingües (en, zh, ko, vi, id) en ui-ux-pro-max.
- Idioma de trabajo con Claude: español.
