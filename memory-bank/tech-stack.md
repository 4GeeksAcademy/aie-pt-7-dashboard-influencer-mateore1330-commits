---
name: tech-stack
description: Tecnologías del dashboard (HTML, Tailwind v4 por CDN, Charts.css, Geist), cómo previsualizarlo y herramientas de trabajo y validación
last_verified: 2026-11-20 (sobre el commit a244c9b, cierre de la fase 2)
---

# Stack tecnológico

## La web

| Pieza | Detalle |
|---|---|
| HTML5 | Un solo `index.html`, `lang="es"`, semántico (regla [HT-01](../.agents/rules/html.md)) |
| Tailwind CSS v4 | Por CDN: `<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>`. Tema en un único `<style type="text/tailwindcss">` con `@theme` ([TW-01](../.agents/rules/tailwind.md), [TW-03](../.agents/rules/tailwind.md)) |
| Charts.css 1.2.0 | Por CDN: `https://cdn.jsdelivr.net/npm/charts.css@1.2.0/dist/charts.min.css`. Gráficos como `<table>` ([CH-01](../.agents/rules/charts.md)) |
| Fuentes | Google Fonts con `<link>`: Geist (400, 500, 600, 700) y Geist Mono (400, 500, 600) (`DESIGN.md` §3) |
| JavaScript propio | **Ninguno**. El menú usa `:target` y los filtros, `has-checked:` y `group-has-[…]:` ([TW-02](../.agents/rules/tailwind.md)) |

**Sin dependencias, sin `package.json`, sin Node y sin build.** Lo que hay en el repositorio es lo
que se sirve. Hace falta conexión a internet: Tailwind, Charts.css y las fuentes se cargan por
CDN.

## Vista previa en local

```bash
python3 -m http.server 8000     # en la raíz; abrir http://localhost:8000
```

Se abre en **Brave**, el navegador de Mateo. Si el puerto 8000 está ocupado, usa otro:
`python3 -m http.server 8080 --bind 127.0.0.1`.

El `server.py` de la plantilla también vale, pero necesita Flask (`pip3 install flask`).

## Herramientas

| Herramienta | Para qué | Dónde |
|---|---|---|
| `gitleaks` 8.30 | Hook `pre-commit` contra secretos | `/opt/homebrew/bin/gitleaks`, activado con `git config core.hooksPath .githooks` |
| `gh` | Abrir PR | `/opt/homebrew/bin/gh` |
| `python3 -m http.server` | Vista previa en local | Incluido en macOS |
| Playwright (skill `rx-test-web`) | Capturas a 375, 768, 1024 y 1440 px, `scrollWidth`, menú y filtros | MCP de Playwright |
| Validador Nu de W3C | HTML válido (0 errores, salvo los 2 del bloque `@theme`; ver HT-02) | https://validator.w3.org/nu/ |
| Lighthouse | Accesibilidad (objetivo 100) en la fase 5 | DevTools del navegador |
| Skill `accessibility` | Auditoría WCAG 2.2 | [`.agents/skills/accessibility/`](../.agents/skills/accessibility/SKILL.md) |
