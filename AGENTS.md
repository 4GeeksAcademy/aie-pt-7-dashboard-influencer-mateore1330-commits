# AGENTS.md — Dashboard de Lucía Vega

## 1. Qué es este proyecto

El dashboard de **Lucía Vega (@luvega.daily)**, una influencer de lifestyle y bienestar
**ficticia**: el ejercicio de 4Geeks "Un dashboard sencillo en Tailwind CSS"
(`simple-dashboard-tailwind-css`). Una sola página (`index.html`) que junta sus resultados de
Instagram, TikTok y YouTube en tres bloques: KPIs, drivers y detalle operativo. Se hace **solo
con HTML y Tailwind CSS v4** por CDN, con **Charts.css** para los gráficos. Sin JavaScript propio.

## 2. Qué leer antes de actuar

Antes de analizar, modificar o generar nada, revisa siempre:

1. **Reglas:** [`./.agents/rules`](.agents/rules/). Empieza por
   [`using-rules.md`](.agents/rules/using-rules.md): dice qué otros archivos de reglas leer según lo
   que vayas a tocar. Al terminar, cita los ID de las reglas que has aplicado (por ejemplo, "HT-02,
   TW-04, CH-02, GD-02").
2. **Skills:** [`./.agents/skills`](.agents/skills/): `accessibility`, para auditar contra WCAG 2.2.
3. **Memory bank:** [`./memory-bank`](memory-bank/): qué es el producto, stack, arquitectura,
   progreso por fase y estado actual.

## 3. Fuentes de verdad, por prioridad

| Tema | Manda |
|---|---|
| Todos los textos y todas las cifras | [`CONTENT.md`](CONTENT.md): se copian **tal cual** |
| Todo lo visual: colores, tipografía, estructura, breakpoints, componentes, menú, gráficos | [`DESIGN.md`](DESIGN.md) |
| Quién es la clienta y qué pide | [`BRIEFING.md`](BRIEFING.md) |
| Proporciones, espaciados, orden de las piezas | [`design/`](design/): maqueta, solo referencia; si choca con `DESIGN.md`, vale `DESIGN.md` |

Si algo no está en estos documentos, **se pregunta a Mateo**. No se inventa (regla UR-02).

## 4. El plan y qué fase toca

El plan está en [`PLAN.md`](PLAN.md) y cada fase en [`plans/`](plans/). Para saber qué fase toca:

1. Mira la tabla de fases de `PLAN.md` §4: la primera que no esté **Hecha**. Si está **En
   revisión**, su PR espera a que Mateo lo fusione: no se empieza la siguiente hasta entonces (el
   estado se cambia en la propia rama antes de pedir la revisión, así que lo que manda es la
   fusión, no la tabla).
2. Comprueba que la anterior está fusionada en `main`: `git log origin/main` y
   `gh pr list --state merged`. Si no lo está, no empieces.
3. Contrasta con [`memory-bank/current-state.md`](memory-bank/current-state.md) § "Siguiente fase".
4. Abre `plans/phase-N-*.md`, resume a Mateo lo que vas a hacer y **espera su "sí"** (el silencio no
   es un sí).

## 5. Lo que nunca se hace

- **CSS propio:** ni archivos `.css`, ni reglas en `<style>` (el único `<style
  type="text/tailwindcss">` solo contiene `@theme`), ni atributos **`style=""`** (TW-02, TW-03).
- **JavaScript propio:** ni `<script>` aparte del CDN de Tailwind, ni `on*=`, ni frameworks. El
  menú usa `:target` y los filtros, `has-checked:` (TW-02, A11Y-05, A11Y-06).
- **Tailwind v3:** ni `cdn.tailwindcss.com`, ni `tailwind.config.js`, ni `@tailwind`, ni
  `@apply` (TW-01).
- **Colores fuera del tema:** ni la paleta por defecto (`bg-purple-600`), ni `bg-[#…]` (TW-04).
- **Inventar** textos o cifras que no estén en `CONTENT.md` (UR-02, HT-06).
- **Fusionar un PR** o hacer push a `main`: lo hace siempre Mateo (GD-04).
- **`git commit --no-verify`**: el hook de gitleaks no se salta (GD-03).

## 6. Puesta en marcha tras clonar

```bash
git config core.hooksPath .githooks   # activa el hook de gitleaks (no viaja con el clon)
python3 -m http.server 8000           # vista previa en http://localhost:8000 (en Brave)
```

Hace falta conexión a internet: Tailwind, Charts.css y las fuentes se cargan por CDN. El
`server.py` de la plantilla también sirve la web, pero necesita Flask (`pip3 install flask`).
