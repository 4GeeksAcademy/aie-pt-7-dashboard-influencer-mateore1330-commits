# PLAN — Dashboard de Lucía Vega

> Plan de implementación del ejercicio de 4Geeks "Un dashboard sencillo en Tailwind CSS"
> (`simple-dashboard-tailwind-css`).
>
> Estado del plan: **APROBADO** por Mateo el 20-11-2026.

---

## 1. Qué hay que construir

Un dashboard de una sola página para Lucía Vega (@luvega.daily), una influencer **ficticia**,
que junta sus resultados de Instagram, TikTok y YouTube. Se organiza en tres bloques: KPIs,
drivers y detalle operativo. Se hace **solo con HTML y Tailwind CSS v4** (CDN), con
**Charts.css** para los gráficos.

Fuentes de verdad, por orden de prioridad:

| Documento | Qué decide |
|---|---|
| `CONTENT.md` | Todos los textos y todas las cifras, tal cual |
| `DESIGN.md` | Todo lo visual: colores, tipografía, estructura, breakpoints, componentes, menú, gráficos |
| `BRIEFING.md` | Quién es la clienta y qué pide |
| `design/` | Maqueta aprobada: solo referencia (manda `DESIGN.md`) |

Si algo no está en estos documentos, **se pregunta a Mateo**. No se inventa.

---

## 2. Cómo arrancar una sesión nueva

1. Lee este `PLAN.md` entero y mira la tabla de fases (§4) para saber cuál toca.
2. Si la fase 1 ya está fusionada, lee `AGENTS.md` y sigue lo que indica (reglas, skills y
   memory bank). Si no, lee `BRIEFING.md`, `CONTENT.md` y `DESIGN.md`.
3. Abre el archivo de la fase que toca (`plans/phase-N-*.md`) y sigue sus pasos.
4. **No empieces una fase hasta que la anterior esté fusionada en `main`.** Compruébalo con
   `git log origin/main` y `gh pr list --state merged`.

---

## 3. Forma de trabajo

- **Repositorio:** `4GeeksAcademy/aie-pt-7-dashboard-influencer-mateore1330-commits`. El remoto
  ya está bien configurado: no se crea otro repositorio.
- **Ramas:** `main` y una rama de trabajo por fase, que sale de `main` actualizada. No hay
  `develop` ni GitHub Project: es un ejercicio del bootcamp, igual que Iron Wolf.
- **Commits:** un commit por paso del plan, en inglés y con Conventional Commits (`feat:`,
  `fix:`, `docs:`, `chore:`, `refactor:`, `test:`). Sin coautor. `git add` con rutas explícitas.
  Nunca `--no-verify`.
- **PR:** al terminar la fase, un PR de la rama a `main` con el resumen, los criterios de
  aceptación marcados y cómo se comprobó cada uno.
- **Fusión:** **la hace siempre Mateo.** El agente nunca fusiona ni hace push a `main`.
- **Aprobaciones:** antes de empezar una fase, el agente resume lo que va a hacer y espera el
  "sí" de Mateo. El silencio no es un sí.
- **Restricciones bloqueantes:**
  - **Solo HTML y Tailwind CSS v4**, cargado con
    `<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>`.
  - **Prohibido:** `cdn.tailwindcss.com`, `tailwind.config.js`, `@tailwind`, `@apply` y
    cualquier otra sintaxis de Tailwind v3; CSS propio (archivos `.css` o reglas en `<style>`);
    atributos `style=""`; JavaScript propio (`<script>` aparte del CDN, `on*=`); React, Vue y
    otros frameworks.
  - **Única excepción:** Charts.css por CDN
    (`https://cdn.jsdelivr.net/npm/charts.css@1.2.0/dist/charts.min.css`) para los gráficos.
  - **La configuración del tema** va en un único `<style type="text/tailwindcss">` que solo
    contiene `@theme` (`DESIGN.md` §9).
- **Vista previa en local:** `python3 -m http.server 8000` en la raíz y abrir
  `http://localhost:8000` en Brave, el navegador de Mateo. El `server.py` de la plantilla
  también vale, pero necesita Flask. Hace falta conexión a internet, porque Tailwind, Charts.css
  y las fuentes se cargan por CDN.
- **Pruebas en el navegador:** con la skill `rx-test-web` (Playwright), con capturas a 375,
  768, 1024 y 1440 px.

---

## 4. Fases

| Fase | Archivo | Rama | Resultado | Estado |
|---|---|---|---|---|
| 0 | [`plans/phase-0-setup.md`](plans/phase-0-setup.md) | `chore/phase-0-setup` | `.gitignore`, hook de gitleaks, documentos, maqueta y plan versionados | En revisión |
| 1 | [`plans/phase-1-agent-harness.md`](plans/phase-1-agent-harness.md) | `docs/phase-1-agent-harness` | `AGENTS.md`, `CLAUDE.md`, reglas, memory bank y skill | Pendiente |
| 2 | [`plans/phase-2-html.md`](plans/phase-2-html.md) | `feat/phase-2-html` | `index.html` semántico completo, con todos los textos, tablas y gráficos | Pendiente |
| 3 | [`plans/phase-3-tailwind.md`](plans/phase-3-tailwind.md) | `feat/phase-3-tailwind` | Todo el estilo con Tailwind, mobile-first, con sidebar desde `md` | Pendiente |
| 4 | [`plans/phase-4-menu-filters.md`](plans/phase-4-menu-filters.md) | `feat/phase-4-menu-filters` | Menú hamburguesa con `:target`, filtros de los rankings y foco visible | Pendiente |
| 5 | [`plans/phase-5-verification.md`](plans/phase-5-verification.md) | `chore/phase-5-verification` | Verificación completa, `verification.md` y README de entrega | Pendiente |

Cada fase pasa a **En revisión** en su propia rama, antes de pedir la revisión. Pasa a **Hecha**
en el PR de la fase siguiente, una vez fusionada. Lo que decide si una fase está terminada es la
fusión en `main`, no esta tabla.

---

## 5. Criterios globales de aceptación

Son los 4 criterios de evaluación del enunciado y sus mínimos. Cada uno indica dónde se
construye y cómo se comprueba al final (fase 5).

| # | Criterio | Fase | Cómo se comprueba |
|---|---|---|---|
| 1 | **HTML semántico:** etiquetas estructurales y landmarks correctos, jerarquía clara | 2 | Validador Nu de W3C con 0 errores. `header`, `nav`, `main`, `section` con `aria-labelledby`, `article`, `table` con `caption` y `th scope`, `footer`. Un `h1`, un `h2` por bloque y `h3` por tarjeta, sin saltos |
| 2 | **Tailwind CSS:** solo clases utility, sin CSS propio, buen uso de breakpoints y de flex/grid | 3 y 4 | Búsqueda en el repo: 0 `style=""`, 0 archivos `.css` propios, 0 reglas en `<style>` aparte de `@theme`, 0 apariciones de `cdn.tailwindcss.com`, `@apply`, `@tailwind` o `tailwind.config`. Breakpoints `sm`, `md`, `lg` y `xl` en uso |
| 3 | **Layout y componentes:** los 3 bloques bien separados, jerarquía visual coherente, componentes reutilizables | 2 y 3 | Al menos **3 KPIs** (hay 5), **3 drivers** (hay 5) y **tablas o listados** (3 tablas, alertas y rankings). Todas las tarjetas comparten la misma base de clases (`DESIGN.md` §6). Mateo lo compara con la maqueta |
| 4 | **Diseño responsivo:** funciona en móvil, tablet y escritorio, mobile-first, sin scroll horizontal | 3 y 4 | Capturas a 375, 768, 1024 y 1440 px. A esos 4 anchos, `scrollWidth` igual a `clientWidth`. Menú hamburguesa por debajo de `md` y sidebar desde `md` |

Además, en todas las fases:

- **Ningún texto ni cifra que no venga de `CONTENT.md`.**
- **Ningún color fuera de `DESIGN.md` §2**, ni de la paleta por defecto de Tailwind.
- **Contraste de 4,5:1 o más** en todo el texto (`DESIGN.md` §2).

---

## 6. Decisiones ya tomadas

- Influencer **ficticia**: Lucía Vega, @luvega.daily, lifestyle y bienestar. Datos de ejemplo
  de octubre de 2026, cuadrados con los precios (50, 120 y 80 €) y el 15 % de comisión.
- Tailwind v4 **solo por CDN**, sin build ni Node. El tema se configura con `@theme`.
- Gráficos con **Charts.css**, la única excepción que permite el enunciado.
- **Sin JavaScript propio.** El menú hamburguesa usa `:target`, como en Iron Wolf, y los filtros
  de los rankings usan radios con las variantes `has-checked:` y `group-has-[…]:` de Tailwind.
- Diseño: propuesta **2b · Studio claro morado**. Sidebar desde `md` (768 px) y menú
  hamburguesa por debajo.
- Git simplificado: `main` y una rama por fase, sin `develop` ni GitHub Project.

## 7. Decisiones abiertas (se preguntan a Mateo cuando toque)

- **README de la plantilla (fase 5):** se propone sustituir `README.md` por uno del proyecto en
  español y quitar `README.es.md` y `README.cn.md` de la plantilla, como en Iron Wolf.
- **Publicación (fase 5):** si se publica en GitHub Pages para enseñarlo. No lo pide el
  enunciado.
- **Contradicción del enunciado:** pide "solo Tailwind, sin CSS propio", pero en la entrega
  menciona "el CSS con los estilos y las media queries". Se resuelve con Tailwind (sus
  breakpoints son las media queries) y se explica en el README (fase 5).
