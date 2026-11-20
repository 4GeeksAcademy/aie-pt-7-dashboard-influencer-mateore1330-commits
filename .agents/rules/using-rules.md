---
name: using-rules
description: Qué archivo de reglas leer antes de editar, qué fuente manda y cómo añadir o cambiar reglas
scope: "**"
---

# Uso de las reglas

Reglas para cualquier agente (o persona) que edite este repositorio. Todas se apoyan en un
documento del propio repositorio: `PLAN.md`, `BRIEFING.md`, `CONTENT.md`, `DESIGN.md`,
`design/README.md` o los planes de `plans/`.

## UR-01 · Lee las reglas que correspondan antes de editar

**Regla:** Antes de analizar o modificar un archivo, lee siempre [`git-and-docs.md`](git-and-docs.md) y,
además, los archivos de reglas que correspondan a lo que vas a tocar:

| Si vas a tocar… | Lee también |
|---|---|
| La estructura, los textos o los atributos de `index.html` | [`html.md`](html.md) y [`accessibility.md`](accessibility.md) |
| Las clases de Tailwind o el `<style type="text/tailwindcss">` (`@theme`) | [`tailwind.md`](tailwind.md) y [`accessibility.md`](accessibility.md) |
| Un gráfico (`<table class="charts-css …">`) | [`charts.md`](charts.md), [`tailwind.md`](tailwind.md) y [`accessibility.md`](accessibility.md) |
| El menú hamburguesa o los filtros de los rankings | [`tailwind.md`](tailwind.md), [`accessibility.md`](accessibility.md) y [`html.md`](html.md) |
| `PLAN.md`, `plans/**`, `memory-bank/**`, `AGENTS.md`, `.agents/**`, `README.md` | Solo `git-and-docs.md` y esta regla |

**Por qué:** [`AGENTS.md`](../../AGENTS.md) obliga a revisar `./.agents/rules` antes de actuar,
pero no dice qué archivo aplica a cada tarea. Cada plan de fase lista las reglas que hay que leer
(por ejemplo, [`plans/phase-2-html.md`](../../plans/phase-2-html.md) § "Lee antes").

**✅ Haz:** para añadir la tabla de campañas, lee `git-and-docs.md`, `html.md` y
`accessibility.md`; para darle estilo, además `tailwind.md`.

**❌ Evita:** cambiar el color de una barra sin haber leído `charts.md` y `tailwind.md`.

**Cómo comprobarlo:** al terminar, cita el ID de cada regla aplicada en tu respuesta y en el PR
(por ejemplo, "HT-02, TW-03, CH-02, A11Y-01, GD-02").

## UR-02 · Respeta qué documento manda en cada tema

**Regla:** Cuando dos fuentes no coincidan, manda la de esta tabla. Si algo no está en ninguna,
**se pregunta a Mateo**: no se inventa.

| Tema | Fuente que manda |
|---|---|
| Todos los textos y **todas las cifras** (KPIs, tablas, alertas, rankings, `aria-label`, `<title>`) | [`CONTENT.md`](../../CONTENT.md) |
| Todo lo visual: colores, tipografía, estructura, breakpoints, componentes, menú, gráficos | [`DESIGN.md`](../../DESIGN.md) |
| Quién es la clienta y qué pide | [`BRIEFING.md`](../../BRIEFING.md) |
| Proporciones, espaciados y orden de las piezas | [`design/`](../../design/), solo como referencia: si contradice a `DESIGN.md`, vale `DESIGN.md` |
| Fases, ramas, criterios de aceptación | [`PLAN.md`](../../PLAN.md) y [`plans/`](../../plans/) |

**Por qué:** `PLAN.md` §1 fija este orden y dice "Si algo no está en estos documentos, se
pregunta a Mateo. No se inventa." [`design/README.md`](../../design/README.md) dice que "Manda
`DESIGN.md`" y que "Los textos y las cifras salen de `CONTENT.md`, no de la maqueta".

**✅ Haz:** escribir el periodo como "1–31 oct 2026 · comparado con septiembre" (`CONTENT.md` §1),
aunque la maqueta ponga "vs septiembre".

**❌ Evita:** copiar un texto de la maqueta o rellenar con una cifra "razonable" (un dato de
noviembre, un porcentaje redondeado) que no está en `CONTENT.md`.

**Cómo comprobarlo:** cada texto y cada cifra visible de `index.html` se encuentra literalmente
en `CONTENT.md` (`grep -F "<texto>" CONTENT.md`).

## UR-03 · Toda regla nueva se apoya en un documento del repositorio

**Regla:** Al añadir o cambiar una regla, usa la plantilla de abajo y apóyala en un documento del
repositorio, citando su ruta y su sección. No se aceptan "buenas prácticas" genéricas sin esa
referencia.

**Por qué:** las reglas existen para que cualquier agente continúe solo con lo que hay en el
repositorio (objetivo de [`plans/phase-1-agent-harness.md`](../../plans/phase-1-agent-harness.md)).
Una regla sin fuente no se puede comprobar ni discutir.

**✅ Haz:** "Las tablas van dentro de `overflow-x-auto`. Por qué: `DESIGN.md` §5".

**❌ Evita:** "Escribe clases ordenadas", que no cita nada.

**Cómo comprobarlo:** cada regla de esta carpeta tiene un **Por qué** con una ruta del
repositorio.

## UR-04 · Mantén el `memory-bank` al día al cerrar cada fase

**Regla:** Lee [`memory-bank/`](../../memory-bank/) al empezar. Al cerrar una fase (y siempre que
tu cambio haga falso algo de lo que dice), actualízalo en la misma rama:

| Si cambias… | Actualiza |
|---|---|
| Cualquier fase (al cerrarla) | [`progress.md`](../../memory-bank/progress.md) y [`current-state.md`](../../memory-bank/current-state.md) |
| Archivos, landmarks, bloques, anclas o breakpoints | [`architecture.md`](../../memory-bank/architecture.md) |
| Herramientas, CDN, versiones o forma de previsualizar | [`tech-stack.md`](../../memory-bank/tech-stack.md) |
| El alcance del ejercicio o qué decide cada documento | [`product-overview.md`](../../memory-bank/product-overview.md) |

Actualiza también el campo `last_verified` con la fecha y el commit sobre el que lo comprobaste,
y el estado de la fase en la tabla de `PLAN.md` §4.

**Por qué:** los planes de las fases 2 a 5 terminan con un paso de cierre que pide actualizar
`PLAN.md` y el memory bank (por ejemplo, [`plans/phase-2-html.md`](../../plans/phase-2-html.md)
paso 7). Un agente nuevo decide qué fase toca leyendo esos archivos.

**✅ Haz:** al cerrar la fase 4, anotar en `progress.md` cuál de `md:hidden` y `target:flex` ganó
y cómo se resolvió.

**❌ Evita:** dejar `current-state.md` diciendo que algo falta cuando ya está hecho.

**Cómo comprobarlo:** el PR de cada fase incluye cambios en `PLAN.md`, `progress.md` y
`current-state.md`.

### Plantilla de una regla

```markdown
## <ID> · <Título corto>

**Regla:** qué hacer, en modo imperativo.

**Por qué:** el documento del repositorio que la justifica, con su ruta y sección.

**✅ Haz:** ejemplo correcto.

**❌ Evita:** el error concreto que la regla previene.

**Cómo comprobarlo:** comando o revisión que demuestra que se ha cumplido.
```

Cada archivo de reglas lleva frontmatter con `name`, `description` y `scope`.

## Índice de reglas

| Archivo | Alcance | Reglas |
|---|---|---|
| [`using-rules.md`](using-rules.md) | Todo el repositorio | UR-01 a UR-04 |
| [`html.md`](html.md) | Estructura y textos de `index.html` | HT-01 a HT-06 |
| [`tailwind.md`](tailwind.md) | Clases y tema de `index.html` | TW-01 a TW-07 |
| [`charts.md`](charts.md) | Gráficos de Charts.css | CH-01 a CH-04 |
| [`accessibility.md`](accessibility.md) | `index.html` | A11Y-01 a A11Y-07 |
| [`git-and-docs.md`](git-and-docs.md) | Ramas, commits, PR y documentación | GD-01 a GD-05 |
