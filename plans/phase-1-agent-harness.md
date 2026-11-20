# Fase 1 — Archivos para el agente

> Rama: `docs/phase-1-agent-harness` · PR a `main` · Depende de: fase 0 fusionada

## Objetivo

Que **cualquier agente, en cualquier sesión**, pueda continuar el proyecto solo con lo que hay en
el repositorio: qué se construye, con qué reglas, en qué punto está y qué está prohibido. Se
sigue la misma estructura que en Iron Wolf
(`../aie-pt-7-web-artist-mateore1330-commits/`), adaptada a HTML + Tailwind v4 + Charts.css.

**No se escribe nada del dashboard.**

## Lee antes

- `PLAN.md`, `BRIEFING.md`, `CONTENT.md`, `DESIGN.md` y `design/README.md`.
- Como modelo de formato (no de contenido), en Iron Wolf: `AGENTS.md`, `CLAUDE.md`,
  `.agents/rules/using-rules.md`, `.agents/rules/git-and-docs.md` y `memory-bank/*.md`.

## Entregables

| Archivo | Contenido |
|---|---|
| `AGENTS.md` | Punto de entrada para cualquier agente |
| `CLAUDE.md` | Importa `AGENTS.md` (`@AGENTS.md`), para Claude Code |
| `.agents/rules/*.md` | 6 archivos de reglas con ID |
| `memory-bank/*.md` | 5 archivos de contexto vivo |
| `.agents/skills/accessibility/` | Copiada de Iron Wolf |

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b docs/phase-1-agent-harness
```

### Paso 2 — Reglas en `.agents/rules/`

Cada archivo lleva frontmatter (`name`, `description`, `scope`) y reglas con ID. Cada regla
tiene **Regla**, **Por qué** (con referencia a un documento del repo), **✅ Haz**, **❌ Evita** y
**Cómo comprobarlo**, como en Iron Wolf.

| Archivo | Prefijo | Qué debe cubrir como mínimo |
|---|---|---|
| `using-rules.md` | UR | Qué reglas leer según lo que se toque (tabla). Citar los ID aplicados al terminar. Las reglas nuevas se apoyan en un documento del repo. Actualizar el memory bank al cerrar cada fase. Prioridad de las fuentes: `CONTENT.md` (textos y cifras), `DESIGN.md` (visual), `BRIEFING.md` (clienta), `design/` (referencia). Lo que no esté, se pregunta a Mateo |
| `html.md` | HT | Todo en `index.html`. HTML semántico y landmarks (`DESIGN.md` §4). Jerarquía: un `h1`, un `h2` por bloque, `h3` por tarjeta, sin saltos. Anclas fijas: `contenido`, `cabecera`, `menu`, `resumen`, `plataformas`, `productos`, `campanas`, `alertas`. Tablas con `caption`, `th scope="col"` y `th scope="row"`. Textos y cifras copiados tal cual de `CONTENT.md`. Sangría de 2 espacios |
| `tailwind.md` | TW | **Solo Tailwind v4 por el CDN `@tailwindcss/browser@4`.** Prohibido `cdn.tailwindcss.com`, `tailwind.config.js`, `@tailwind`, `@apply` y cualquier sintaxis de v3; prohibido CSS propio, `style=""` y JavaScript propio. Un único `<style type="text/tailwindcss">` que solo contiene `@theme` con los tokens de `DESIGN.md` §2–3. Solo colores del tema (nada de `bg-purple-600` ni `bg-[#…]`). Mobile-first: clases base para móvil y después `sm:`, `md:`, `lg:`, `xl:`. Sin tamaños en píxeles salvo en valores arbitrarios justificados. Misma base de clases para componentes iguales (`DESIGN.md` §6). Ningún scroll horizontal: tablas en `overflow-x-auto` y `min-w-0` en sus contenedores |
| `charts.md` | CH | Charts.css 1.2.0 por CDN, la única excepción. Cada gráfico es una `<table class="charts-css …">` con `caption`. Tamaño y color con propiedades arbitrarias de Tailwind (`[--size:0.63]`, `[--color:var(--color-morado-500)]`), nunca con `style=""`. Tipos y colores: `DESIGN.md` §8. Las cifras siempre visibles, no solo el color |
| `accessibility.md` | A11Y | Contraste de 4,5:1 o más con los pares de `DESIGN.md` §2 (`rosa-500` nunca como texto sobre claro). Lo decorativo con `aria-hidden="true"`. Enlace "Saltar al contenido". Foco visible siempre. Zonas táctiles de 44 px o más. Menú con `:target` y lo que se pierde (`DESIGN.md` §7). Filtros con `fieldset` y `legend`. Usar la skill `accessibility` para auditar |
| `git-and-docs.md` | GD | `main` y una rama por fase (`tipo/phase-N-descripcion`). Conventional Commits en inglés, un commit por paso, sin coautor. `git add` con rutas explícitas. Nunca `--no-verify`. PR a `main` con los criterios marcados. **El agente no fusiona.** Activar el hook tras clonar: `git config core.hooksPath .githooks`. La documentación se escribe en español |

### Paso 3 — Memory bank en `memory-bank/`

Cada archivo lleva frontmatter (`name`, `description`, `last_verified`).

| Archivo | Contenido |
|---|---|
| `product-overview.md` | El ejercicio (enunciado resumido, mínimos, entregable y los 4 criterios de evaluación); Lucía Vega es **ficticia**; para quién es el panel; qué decide cada documento |
| `tech-stack.md` | HTML + Tailwind v4 por CDN + Charts.css 1.2.0 + Google Fonts (Geist y Geist Mono). Sin build, sin Node, sin JavaScript propio. Herramientas: gitleaks, `python3 -m http.server`, Playwright (skill `rx-test-web`), validador Nu de W3C |
| `architecture.md` | Estructura **prevista** del repo y de `index.html` (landmarks, bloques, anclas, breakpoints), según `DESIGN.md` §4–5 |
| `progress.md` | Fases hechas y lo aprendido en cada una (se rellena al cerrar cada fase) |
| `current-state.md` | Fase actual, siguiente fase y decisiones abiertas (`PLAN.md` §7) |

### Paso 4 — Skill

Copiar `.agents/skills/accessibility/` de Iron Wolf tal cual. No hace falta la de SEO: el
enunciado no la pide.

### Paso 5 — `AGENTS.md` y `CLAUDE.md`

`AGENTS.md`, con las mismas secciones que en Iron Wolf:

1. Qué es este proyecto.
2. Qué leer antes de actuar: reglas, skill y memory bank.
3. Fuentes de verdad, por prioridad.
4. El plan y qué fase toca.
5. Lo que nunca se hace: CSS propio, `style=""`, JavaScript propio, `cdn.tailwindcss.com` o
   sintaxis de v3, inventar textos o cifras, fusionar un PR, `--no-verify`.
6. Puesta en marcha tras clonar: activar el hook y la vista previa local.

`CLAUDE.md` contiene solo `@AGENTS.md`.

### Paso 6 — Prueba en frío

Con una sesión nueva de agente que solo lea el repo, hacer 4 preguntas y comprobar que las
respuestas salen de los documentos:

1. ¿Qué fase toca y qué hay que hacer?
2. ¿Puedo usar `bg-purple-600` o un `style="width: 60%"` para una barra?
3. ¿De dónde saco el texto de la alerta de caída?
4. ¿Cómo se abre el menú en móvil sin JavaScript?

Si alguna respuesta falla, se corrige la regla o el documento y se anota en
`memory-bank/progress.md`.

### Paso 7 — Push y PR

Estado de la fase 1 en `PLAN.md` §4: **En revisión**; el de la fase 0, **Hecha**.

```bash
git push -u origin docs/phase-1-agent-harness
gh pr create --base main --title "docs: phase 1 – agent harness" --body "<resumen y criterios>"
```

## Criterios de aceptación

- [ ] Existen `AGENTS.md`, `CLAUDE.md`, las 6 reglas, los 5 archivos del memory bank y la skill.
- [ ] Cada regla tiene ID, "Por qué" con referencia a un documento y "Cómo comprobarlo".
- [ ] La prueba en frío responde bien las 4 preguntas (resultado en el PR).
- [ ] Commits en inglés con tipo, uno por paso.
- [ ] El PR va contra `main` y no está fusionado.

## Fuera de alcance

- Escribir `index.html`.
