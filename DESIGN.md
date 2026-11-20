# DESIGN — Sistema visual del dashboard de Lucía Vega

> Diseño **aprobado** por Mateo el 20-11-2026: "propuesta 2b · Studio claro morado", con su
> versión móvil y el menú hamburguesa.
> Maqueta de referencia (privada): https://claude.ai/artifact/TAENwNd12tfrvyC7PzMYhN → mesas
> "Propuesta 2b · Studio claro morado (elegida)", "2b · Móvil (pulsa Menú)" y
> "2b · Móvil, menú abierto". Las otras propuestas del lienzo están **descartadas**.
>
> Este documento manda sobre la maqueta: si algo no coincide, vale lo que diga aquí. Los textos
> y las cifras están en `CONTENT.md`; la clienta, en `BRIEFING.md`.
>
> Restricción: **solo HTML + Tailwind CSS v4** (CDN `@tailwindcss/browser@4`) y **Charts.css**
> para los gráficos. Ni CSS propio, ni JavaScript propio, ni otros frameworks, ni
> `cdn.tailwindcss.com`, ni sintaxis de Tailwind v3 (`tailwind.config.js`, `@apply`,
> `@tailwind base`…).

---

## 1. Concepto

**Un estudio de creadora, claro y preciso.** Base blanca y lavanda muy suave, tarjetas blancas
con bordes finos, cifras grandes en tipografía monoespaciada y un morado intenso como color
principal, con toques de rosa. Recuerda a las herramientas para creadores de ahora, no a un
panel de administración genérico.

Tres reglas:

1. **El morado manda y el rosa acentúa.** El morado marca lo importante (comisiones, selección,
   cifras destacadas); el rosa, lo que hay que mirar (ventas, YouTube, lo negativo).
2. **Las cifras se leen al momento:** grandes, en Geist Mono, con el cambio respecto a
   septiembre justo debajo.
3. **Cada gráfico explica algo** (paso entre etapas, retorno, reparto) y lleva sus cifras
   escritas: nunca depende solo del color.

---

## 2. Colores

Se definen como variables de tema de Tailwind v4 (`@theme`, §9) y generan sus clases
(`bg-morado-500`, `text-rosa-700`…). No se usa ningún color fuera de esta lista ni la paleta
por defecto de Tailwind.

| Variable (`--color-…`) | Valor | Uso |
|---|---|---|
| `fondo` | `#F8F7FB` | Fondo de la página, cabeceras de tabla |
| `superficie` | `#FFFFFF` | Tarjetas, sidebar, barra superior en móvil |
| `linea` | `#E7E3F3` | Bordes de tarjetas, separadores de tablas, rejilla de KPIs |
| `lavanda-50` | `#F1EDFC` | Pistas de las barras, chips de actividad, tarjetas de producto, fondo de los filtros |
| `lavanda-100` | `#EDE7FF` | Enlace activo de la sidebar, etiqueta "Superada" |
| `lavanda-200` | `#D9D0FB` | Texto secundario dentro del menú móvil |
| `lavanda-300` | `#B9A6F7` | Etapa "Clics" del embudo |
| `lavanda-400` | `#CFC2FB` | Borde de la alerta "Pico" |
| `lavanda-pico` | `#F4F0FF` | Fondo de la alerta "Pico" |
| `morado-500` | `#673DE6` | **Color principal**: tarjeta de comisiones, logo, filtro activo, Instagram, etapa "Interacciones", producto A |
| `morado-600` | `#5B2FD6` | Texto destacado en morado: subidas (▲), ROI, ★, porcentajes de paso |
| `morado-700` | `#4B23C2` | Texto de la etiqueta "Superada" |
| `morado-800` | `#4A3790` | Líneas dentro del menú móvil |
| `morado-900` | `#2F1C6A` | Fondo del menú móvil, TikTok, etapa "Alcance", producto C |
| `rosa-50` | `#FFF0F4` | Fondo de la alerta "Caída" |
| `rosa-100` | `#FFE3EB` | Fondo de la etiqueta "Por debajo" |
| `rosa-200` | `#F7B9CB` | Borde de la alerta "Caída" |
| `rosa-300` | `#FF7BA3` | Números y flechas del menú móvil (sobre `morado-900`) |
| `rosa-500` | `#FC5185` | **Acento**: YouTube, etapa "Ventas", producto B, etiqueta "+12 %", botón "Cerrar". **Nunca como texto sobre fondo claro** |
| `rosa-700` | `#C81E52` | Texto en rosa sobre claro: bajadas (▼), "Caída", números del ranking |
| `rosa-800` | `#B0174A` | Texto de la etiqueta "Por debajo" |
| `tinta` | `#1D1B2C` | Texto principal; texto sobre `rosa-500` |
| `tinta-suave` | `#3E3A52` | Texto secundario fuerte (alertas, filtros sin elegir) |
| `gris` | `#5F5A73` | Texto secundario, etiquetas, pies de tabla |

**Colores de cada red** (se distinguen también por claridad, no solo por tono):
Instagram `morado-500` (medio) · TikTok `morado-900` (oscuro) · YouTube `rosa-500` (claro).

**Contraste comprobado (WCAG, 20-11-2026):** todas las combinaciones de texto superan 4,5:1.
Las más justas: `rosa-700` sobre `rosa-50` (5,05), `tinta` sobre `rosa-500` (5,34),
`rosa-300` sobre `morado-900` (5,76), `gris` sobre `lavanda-50` (5,71). `rosa-500` sobre
blanco da 3,16: por eso **no se usa como texto** sobre fondo claro.

---

## 3. Tipografía

Google Fonts con `<link>` en el `<head>`: **Geist** (400, 500, 600, 700) y **Geist Mono**
(400, 500, 600). En `@theme`: `--font-sans` = Geist y `--font-mono` = Geist Mono, con
`system-ui, sans-serif` y `monospace` de respaldo.

| Elemento | Fuente | Tamaño (móvil → escritorio) | Peso |
|---|---|---|---|
| `h1` "Hola, Lucía" | Geist | `text-3xl` → `md:text-4xl` | 600, `tracking-tight` |
| `h2` de bloque ("01 · Resumen del mes") | Geist Mono | `text-xs` / `text-sm`, mayúsculas, `tracking-widest` | 500, `gris` |
| `h3` de tarjeta | Geist | `text-lg` | 600 |
| Cifra de KPI | Geist Mono | `text-3xl` → `2xl:text-4xl` | 600, `tracking-tighter` |
| Cifras de gráficos y tablas | Geist Mono | `text-sm` / `text-xs` | 400–600 |
| Texto normal | Geist | `text-sm` / `text-base` | 400–500 |

Se usan las escalas de Tailwind, nunca tamaños en píxeles.

---

## 4. Estructura

```
Móvil y tablet pequeña (< md)          Tablet y escritorio (≥ md)
┌──────────────────────────┐           ┌────────┬───────────────────────────┐
│ LV Lucía Vega    [≡ Menú]│ (fija)    │ LV     │ Hola, Lucía      periodo  │
├──────────────────────────┤           │ Lucía  ├───────────────────────────┤
│ Hola, Lucía · periodo    │           │        │ 01 KPIs                   │
│ 01 KPIs                  │           │ Resumen│ 02 Drivers                │
│ 02 Drivers               │           │ Plataf.│ 03 Detalle                │
│ 03 Detalle               │           │ Produc.│                           │
└──────────────────────────┘           │ Campañ.│                           │
                                       │ Alertas│                           │
                                       └────────┴───────────────────────────┘
```

- **Landmarks:** enlace "Saltar al contenido" → `<aside>` con `<nav>` (sidebar) y, en móvil,
  `<header>` con el botón "Menú" y el `<nav>` del panel → `<main>` con tres `<section>` (una por
  bloque, cada una con su `h2`) → `<footer>`.
- **Anclas del menú:** `#resumen` (bloque 1), `#plataformas` (bloque 2, empieza por el
  rendimiento por plataforma), `#productos` (tarjeta de rendimiento por producto),
  `#campanas` (tabla de campañas), `#alertas` (alertas). Llevan `scroll-mt-*` para que la barra
  fija del móvil no tape el título.

---

## 5. Breakpoints (mobile-first)

| Rango | Qué cambia |
|---|---|
| Base (< 640 px) | Barra superior fija con "Menú". Todo en una columna. KPIs en rejilla de 2 columnas, con comisiones ocupando las 2 |
| `sm` (≥ 640 px) | Más aire (`px-6`). Las tarjetas de producto pasan a 3 columnas |
| `md` (≥ 768 px) | **Aparece la sidebar** (fija, `w-56`, alto de pantalla) y desaparecen la barra superior y el menú hamburguesa. Cabecera con el periodo a la derecha |
| `lg` (≥ 1024 px) | Alertas en 3 columnas. **Todas las tablas caben sin scroll**: celdas compactas (`text-xs`, `px-1.5`) y títulos de columna que pueden ocupar 2 líneas |
| `xl` (≥ 1280 px) | KPIs en una sola franja de **5 columnas iguales**, como la maqueta. Drivers en 2 columnas: embudo y plataforma lado a lado; producto y engagement ocupan las 2. Campañas y productos, una debajo de otra (lado a lado no caben). Tablas con `text-sm` y `px-3` |

**Nunca hay scroll horizontal de la página:** las tablas van dentro de una caja
`overflow-x-auto` y se desplazan dentro de su tarjeta. Los elementos de rejilla y flex que
contienen tablas llevan `min-w-0`.

**Tablas por debajo de `lg`:** todas tienen un ancho mínimo (`min-w-3xl`) y se desplazan, para
que el comportamiento sea igual en todas. Como en macOS e iOS la barra de scroll no se ve hasta
que se usa, cada una lleva encima el aviso "Desliza para ver toda la tabla →" (`CONTENT.md` §0) y
un degradado `superficie` en el borde derecho, los dos solo por debajo de `lg` y con
`aria-hidden="true"`. Desde `lg` caben todas sin scroll.

> Cambios aprobados por Mateo el 20-11-2026, tras revisar la fase 4: KPIs iguales (antes
> comisiones ocupaba el doble), tablas sin scroll en escritorio con aviso en móvil, y las alertas
> dentro de una tarjeta.

---

## 6. Componentes

| Componente | Cómo es |
|---|---|
| **Tarjeta** | `bg-superficie`, borde 1 px `linea`, `rounded-2xl`, `p-6`. Título `h3` y subtítulo en `gris`. Todas las tarjetas comparten esta base |
| **Franja de KPIs** | Una rejilla con `gap-px` sobre fondo `linea` y `rounded-2xl` con `overflow-hidden`: las celdas parecen separadas por líneas finas. Cada KPI: nombre (`gris`), cifra (Geist Mono) y cambio (▲ en `morado-600`, ▼ en `rosa-700`) con su detalle. **Comisiones**: fondo `morado-500`, texto blanco y la etiqueta "▲ +12 %" en píldora `rosa-500` con texto `tinta` |
| **Sidebar** (≥ md) | `bg-superficie`, borde derecho `linea`. Logo: cuadrado `morado-500` con "LV" en Geist Mono blanco, nombre y @usuario. Enlaces de 44 px o más; el activo con fondo `lavanda-100`, texto `morado-900` y un punto `morado-500` delante |
| **Menú en móvil (hamburguesa)** | Ver §7 |
| **Embudo de ventas** | Gráfico de columnas (§8) con 4 etapas: Alcance `morado-900`, Interacciones `morado-500`, Clics `lavanda-300` y Ventas `rosa-500`. Debajo, cada etapa con su cifra y, en `morado-600`, el porcentaje de paso desde la anterior. Nota: "Barras en escala orientativa, no proporcional" |
| **Rendimiento por plataforma** | Gráfico de barras horizontales (§8), una por red con su color, sobre una pista `lavanda-50`. Encima de cada barra: red, comisión y ROI en `morado-600`. Pie con los costes |
| **Rendimiento por producto** | Tres tarjetas pequeñas `lavanda-50` (producto y precio, comisión en Geist Mono, ventas y engagement) ordenadas por comisión, y debajo una barra apilada (§8) con el reparto de los 3.840 € |
| **Engagement y actividad** | Tabla compacta (me gusta, comentarios, compartidos, guardados, engagement) y debajo chips `lavanda-50` con lo publicado en cada red |
| **Alertas** | Una tarjeta (la base común) con el título "Alertas" y, dentro, tres tarjetas con su etiqueta en Geist Mono mayúsculas: **Caída** (fondo `rosa-50`, borde `rosa-200`, etiqueta `rosa-700`, "▼"), **Pico** (fondo `lavanda-pico`, borde `lavanda-400`, etiqueta `morado-600`, "▲") y **Anomalía** (blanco, borde `linea`, etiqueta `tinta-suave`, "◆"). Nada de bordes laterales de color |
| **Tablas** | `<table>` con `<caption>` (puede ir oculta con `sr-only` si el `h3` ya la nombra), `<th scope="col">` y `<th scope="row">`. Cabecera en Geist Mono `text-xs` sobre `fondo`; filas separadas por `linea`; cifras en Geist Mono. Lo mejor de cada métrica, en `morado-600` y con ★ |
| **Etiquetas de estado** | Píldoras `rounded-full`: "Superada" (`lavanda-100` / `morado-700`), "Por debajo" (`rosa-100` / `rosa-800`), "Casi" (`lavanda-50` / `tinta-suave`) |
| **Rankings con filtros** | Grupo de 4 filtros sobre una cápsula `lavanda-50`; el elegido en `morado-500` con texto blanco. Debajo, el listado de 3 puestos: número en Geist Mono `rosa-700` ("01"), título en negrita y valor en `gris` |

---

## 7. Menú en móvil (hamburguesa)

Igual que en la web de Iron Wolf (web-artist), adaptado a esta paleta:

- **Por debajo de `md`** la sidebar no se ve. Arriba queda una **barra fija** (`fixed`,
  `bg-superficie`, borde inferior `linea`) con el logo y el nombre a la izquierda y el botón
  **"Menú"** a la derecha: icono de tres rayas (SVG en línea, `aria-hidden="true"`) y el texto
  "Menú", borde `linea`, `rounded-lg`, 44 px de alto o más.
- **Al abrirlo**, un panel `morado-900` cubre **toda la pantalla**:
  - Arriba, el logo (cuadrado blanco con "LV" en `morado-900`) y, en el sitio de "Menú", el
    botón **"✕ Cerrar"**: relleno `rosa-500`, texto `tinta`, mismo alto. El "✕" va oculto al
    lector de pantalla.
  - Debajo, los 5 enlaces, uno por línea, de 60 px de alto, separados por líneas `morado-800`,
    en blanco y `text-xl`. Delante de cada uno, su número ("01 /" … "05 /") en Geist Mono
    `rosa-300`; a la derecha, una flecha → `rosa-300`. Números y flechas son decorativos
    (`aria-hidden="true"`).
  - Abajo del todo, @luvega.daily en blanco y el periodo en Geist Mono `lavanda-200`.
  - Mientras está abierto, la página no hace scroll.
- **Se cierra** con "Cerrar", que te deja donde estabas, o al pulsar una sección, que lleva a
  ella. En `md` y más el panel no existe a la vista: se ve la sidebar.

**Cómo se hace sin JavaScript (técnica `:target`, como en web-artist):** "Menú" es un enlace a
`#menu`; el panel tiene `id="menu"` y las clases `hidden target:flex`. "Cerrar" apunta a la
propia barra fija (`#cabecera`), así que el menú se cierra sin mover la página. Al pulsar una
sección, `#menu` deja de estar apuntado y el panel desaparece. El bloqueo de scroll se hace con
`has-[#menu:target]:overflow-hidden` en el `<body>`.

**Lo que se pierde** (aceptado, igual que en web-artist): el lector de pantalla oye "enlace" en
vez de "botón, expandido o contraído"; la tecla Esc no cierra el menú; la dirección muestra
`#menu` mientras está abierto, y el botón "Atrás" lo cierra.

---

## 8. Gráficos con Charts.css

Charts.css se carga por CDN con un `<link>` (versión fijada en el plan). Es la **única**
excepción a "solo Tailwind" que permite el enunciado. Cada gráfico es una `<table>` con
`<caption>`, así que también se lee bien con lector de pantalla.

| Gráfico | Tipo de Charts.css |
|---|---|
| Embudo de ventas | `column` con `show-labels` y `data-spacing-*` |
| Rendimiento por plataforma | `bar` con `show-labels` |
| Reparto de comisiones por producto | `bar multiple stacked` (una sola fila con 3 datos) |

- **Tamaño y color, con clases de Tailwind**, no con `style`: `[--size:0.63]` para el valor
  y `[--color:var(--color-morado-500)]` para el color, como propiedades arbitrarias en cada
  `<td>`. Así no hace falta CSS propio.
- El aspecto puede variar un poco respecto a la maqueta (está dibujada con `div`), pero se
  mantienen los colores, el orden, las cifras visibles y las proporciones.

---

## 9. Configuración de Tailwind v4

Un único bloque en el `<head>`, después del `<script>` del CDN:

```html
<style type="text/tailwindcss">
  @theme {
    --font-sans: "Geist", system-ui, sans-serif;
    --font-mono: "Geist Mono", monospace;
    --color-fondo: #F8F7FB;
    /* … el resto de colores de §2 … */
  }
</style>
```

- **Solo contiene `@theme`**: son ajustes de Tailwind (sus variables de tema), no reglas de CSS.
  No hay `@apply`, ni selectores, ni `@layer` propios.
- **Comprobación:** en ningún archivo aparecen `cdn.tailwindcss.com`, `tailwind.config`,
  `@tailwind` ni `@apply`.

---

## 10. Accesibilidad

- Contraste: §2. Los gráficos llevan sus cifras escritas y los colores de las redes se
  distinguen por claridad.
- Zonas táctiles de 44 px o más (enlaces de la sidebar y del menú, botón "Menú", filtros).
- Foco visible en todos los enlaces y filtros (`focus-visible:outline-2
  focus-visible:outline-morado-500 focus-visible:outline-offset-2`).
- Filtros de los rankings: `<fieldset>` con `<legend class="sr-only">Elegir ranking</legend>` y
  radios reales ocultos con `sr-only` dentro de su `<label>`. El seleccionado se pinta con
  `has-checked:` y cada listado se muestra según el radio marcado.
- Iconos decorativos con `aria-hidden="true"`; ▲ ▼ ◆ ★ van acompañados de texto.
