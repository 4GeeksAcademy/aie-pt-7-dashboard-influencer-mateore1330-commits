---
name: tailwind
description: Solo Tailwind CSS v4 por CDN — sin sintaxis de v3, sin CSS propio, sin style="", sin JavaScript propio; tema en @theme, colores del tema, mobile-first y sin scroll horizontal
scope: index.html (clases, <head> y <style type="text/tailwindcss">)
---

# Reglas de Tailwind CSS v4

Aplican a cualquier clase, al `<head>` y al bloque de tema de `index.html`. Para los gráficos,
lee también [`charts.md`](charts.md); para contraste y foco, [`accessibility.md`](accessibility.md).

## TW-01 · Solo Tailwind v4 por el CDN `@tailwindcss/browser@4`

**Regla:** Tailwind se carga **solo** con:

```html
<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
```

Está **prohibido** todo lo que es de Tailwind v3 o de un build:

- `cdn.tailwindcss.com` (es el CDN de v3).
- `tailwind.config.js` (o `.ts`, `.cjs`), `postcss.config.*`, `package.json`.
- Las directivas `@tailwind base/components/utilities`, `@apply`, `@layer`, `@config`.
- Clases de v3 que cambiaron en v4 (por ejemplo, `bg-opacity-*`, `flex-shrink-0`,
  `overflow-ellipsis`): se usa la forma de v4 (`bg-morado-500/50`, `shrink-0`, `text-ellipsis`).

**Por qué:** `PLAN.md` §3 (restricción bloqueante: "Solo HTML y Tailwind CSS v4, cargado con
`<script src=…@tailwindcss/browser@4>`" y "Prohibido: `cdn.tailwindcss.com`, `tailwind.config.js`,
`@tailwind`, `@apply` y cualquier otra sintaxis de Tailwind v3"). `DESIGN.md` (cabecera) y §9.

**✅ Haz:** el `<script>` del CDN de jsDelivr, una sola vez, en el `<head>` (después de
Charts.css, `plans/phase-2-html.md` paso 2).

**❌ Evita:** copiar un ejemplo antiguo con `<script src="https://cdn.tailwindcss.com">` y un
`tailwind.config = {…}`.

**Cómo comprobarlo:**

```bash
grep -rnE "cdn\.tailwindcss\.com|tailwind\.config|@tailwind|@apply|@layer|@config" --exclude-dir=.git --exclude-dir=design --exclude="*.md" .   # sin resultados
```

## TW-02 · Sin CSS propio, sin `style=""` y sin JavaScript propio

**Regla:** En `index.html` no puede haber:

- Ningún atributo `style="…"`.
- Ningún `<style>` salvo el único `<style type="text/tailwindcss">` de TW-03.
- Ningún archivo `.css` propio ni `<link rel="stylesheet">` salvo Charts.css y Google Fonts.
- Ningún `<script>` salvo el del CDN de Tailwind; ningún atributo `on*=` (`onclick=`…); ninguna
  URL `javascript:`.
- Ningún framework (React, Vue, Alpine, htmx…).

El menú y los filtros se hacen con variantes de Tailwind (`target:`, `has-checked:`,
`group-has-[…]:`), no con JavaScript. Si algo parece necesitar CSS o JavaScript propios, **se
pregunta a Mateo** antes de buscar otra salida.

**Por qué:** `PLAN.md` §3 ("Prohibido: … CSS propio (archivos `.css` o reglas en `<style>`);
atributos `style=""`; JavaScript propio (`<script>` aparte del CDN, `on*=`); React, Vue y otros
frameworks") y §6 ("Sin JavaScript propio. El menú hamburguesa usa `:target` … y los filtros …
`has-checked:` y `group-has-[…]:`"). Criterio 2 de `PLAN.md` §5.

**✅ Haz:** el tamaño de una barra con la clase `[--size:0.63]` (ver [CH-02](charts.md)).

**❌ Evita:** `<td style="--size: 0.63">`, un `<script>` para cambiar de filtro o un
`onclick="…"` en "Menú".

**Cómo comprobarlo:**

```bash
grep -nE 'style="|<style>|<style [^t]' index.html     # sin resultados
grep -n "<script" index.html                          # una línea: el CDN de Tailwind
grep -nE ' on[a-z]+=|javascript:' index.html          # sin resultados
```

## TW-03 · Un único `<style type="text/tailwindcss">` que solo contiene `@theme`

**Regla:** El tema va en un único bloque, en el `<head>`, después del `<script>` del CDN. Dentro
solo hay `@theme { … }` con:

- `--font-sans: "Geist", system-ui, sans-serif;` y `--font-mono: "Geist Mono", monospace;`
- **Todos** los colores de `DESIGN.md` §2, con su nombre y su valor exactos
  (`--color-fondo: #F8F7FB;`, `--color-morado-500: #673DE6;`…).

Ni selectores, ni `@apply`, ni `@layer`, ni `@utility`, ni `@custom-variant`.

**Por qué:** `PLAN.md` §3 ("La configuración del tema va en un único
`<style type="text/tailwindcss">` que solo contiene `@theme`") y `DESIGN.md` §9 ("Solo contiene
`@theme`: son ajustes de Tailwind … no reglas de CSS").

**✅ Haz:** copiar los 24 colores de la tabla de `DESIGN.md` §2 como `--color-<variable>`.

**❌ Evita:** añadir `.tarjeta { … }` o `body { … }` dentro del bloque, o un color que no está
en §2.

**Cómo comprobarlo:** `grep -c "<style" index.html` devuelve 1, y entre `<style` y `</style>`
solo hay `@theme`, `--font-*` y `--color-*`.

## TW-04 · Solo colores del tema

**Regla:** Todo color sale de las clases que genera el tema (`bg-morado-500`, `text-rosa-700`,
`border-linea`…), más `white`, `transparent` y `current`. Nunca la paleta por defecto de
Tailwind (`purple-`, `violet-`, `pink-`, `gray-`, `slate-`, `zinc-`…) ni colores arbitrarios
(`bg-[#673DE6]`, `text-[rgb(…)]`). En las propiedades de Charts.css, el color se toma del tema:
`[--color:var(--color-morado-500)]`.

**Por qué:** `DESIGN.md` §2 ("No se usa ningún color fuera de esta lista ni la paleta por defecto
de Tailwind") y `PLAN.md` §5 ("Ningún color fuera de `DESIGN.md` §2").

**✅ Haz:** `bg-lavanda-50 text-gris` en la cápsula de los filtros.

**❌ Evita:** `bg-purple-600` porque "se parece" al morado, o `bg-[#673DE6]`.

**Cómo comprobarlo:**

```bash
grep -noE '\b(bg|text|border|outline|ring|fill|stroke|from|to|via|divide|decoration|shadow)-(red|orange|amber|yellow|lime|green|emerald|teal|cyan|sky|blue|indigo|violet|purple|fuchsia|pink|rose|slate|gray|zinc|neutral|stone|black)-' index.html   # sin resultados
grep -nE '\[#|\[rgb|\[hsl|\[oklch' index.html                                                  # sin resultados
```

## TW-05 · Mobile-first, con los breakpoints de `DESIGN.md` §5

**Regla:** Las clases sin prefijo son las del **móvil**; lo que cambia en pantallas mayores se
añade con `sm:` (640 px), `md:` (768 px), `lg:` (1024 px) y `xl:` (1280 px), exactamente como
describe `DESIGN.md` §5. No se usan `max-*:` para construir el móvil "hacia abajo". Tamaños y
espacios con las escalas de Tailwind (`p-6`, `text-sm`, `w-56`), nunca en píxeles; un valor
arbitrario (`[…]`) solo si la escala no lo tiene, y se justifica en el PR.

**Por qué:** `DESIGN.md` §5 ("Breakpoints (mobile-first)") y §3 ("Se usan las escalas de
Tailwind, nunca tamaños en píxeles"). Criterio 4 de `PLAN.md` §5 ("mobile-first") y criterio 2
("Breakpoints `sm`, `md`, `lg` y `xl` en uso"). `BRIEFING.md`: Lucía lo mira "sobre todo en el
móvil".

**✅ Haz:** la sidebar con `hidden md:flex md:w-56`, y los KPIs con `grid-cols-2 lg:grid-cols-3
xl:grid-cols-6`.

**❌ Evita:** `flex max-md:hidden`, `w-[224px]` o `text-[13px]`.

**Cómo comprobarlo:** `grep -oE '\b(sm|md|lg|xl):' index.html | sort | uniq -c` muestra los 4
prefijos; `grep -nE '\[[0-9.]+px\]' index.html` solo devuelve valores justificados en el PR.

## TW-06 · Componentes iguales, misma base de clases

**Regla:** Todos los elementos del mismo tipo comparten **la misma base de clases** de
`DESIGN.md` §6, en el mismo orden: tarjeta (`bg-superficie border border-linea rounded-2xl p-6`),
`h2` de bloque, `h3` de tarjeta, cifra de KPI, etiqueta de estado, cabecera y filas de tabla,
enlace de la sidebar y del menú, filtro. Las diferencias (el KPI de comisiones, el color de cada
alerta) se añaden **después** de la base.

**Por qué:** criterio 3 de `PLAN.md` §5 ("Todas las tarjetas comparten la misma base de clases
(`DESIGN.md` §6)"); `DESIGN.md` §6 ("Todas las tarjetas comparten esta base");
[`plans/phase-3-tailwind.md`](../../plans/phase-3-tailwind.md) paso 3 ("idénticas en todos los
elementos del mismo tipo").

**✅ Haz:** copiar la cadena de clases de la primera tarjeta en todas las demás y añadir al final
lo propio.

**❌ Evita:** una tarjeta con `rounded-xl p-5` y otra con `rounded-2xl p-6`.

**Cómo comprobarlo:** `grep -c 'bg-superficie border border-linea rounded-2xl p-6' index.html`
coincide con el número de tarjetas.

## TW-07 · Nunca hay scroll horizontal

**Regla:** La página no se desplaza en horizontal en ningún ancho. Cada tabla va dentro de una
caja `overflow-x-auto` (con la tabla en `min-w-*` si lo necesita) y se desplaza **dentro** de su
tarjeta. Los elementos de rejilla y flex que contienen tablas o textos largos llevan `min-w-0`.

**Por qué:** `DESIGN.md` §5 ("Nunca hay scroll horizontal de la página: las tablas van dentro de
una caja `overflow-x-auto` … Los elementos de rejilla y flex que contienen tablas llevan
`min-w-0`") y criterio 4 de `PLAN.md` §5 ("`scrollWidth` igual a `clientWidth`").

**✅ Haz:** `<div class="overflow-x-auto"><table class="min-w-2xl …">` dentro de un `<article
class="… min-w-0">`.

**❌ Evita:** dejar la tabla de plataformas (10 columnas) suelta en una tarjeta de la rejilla.

**Cómo comprobarlo:** con Playwright (skill `rx-test-web`), a 375, 768, 1024 y 1440 px,
`document.documentElement.scrollWidth === document.documentElement.clientWidth` es `true`.
