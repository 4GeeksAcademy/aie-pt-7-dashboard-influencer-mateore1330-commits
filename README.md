# Dashboard de Lucía Vega

Panel de resultados de octubre de 2026 de **Lucía Vega (@luvega.daily)**, una creadora de
contenido de lifestyle y bienestar **ficticia**. Junta sus datos de Instagram, TikTok y YouTube en
una sola página con tres bloques: **KPIs**, **drivers** (qué explica el resultado) y **detalle
operativo**. Todas las cifras son datos de ejemplo.

Ejercicio de 4Geeks Academy: **"Un dashboard sencillo en Tailwind CSS"**.

## Cómo verlo

No hace falta instalar nada ni compilar. En la raíz del repositorio:

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```

Abre http://127.0.0.1:8080. Hace falta conexión a internet, porque Tailwind CSS, Charts.css y las
fuentes se cargan por CDN.

Para ver el diseño responsive, estrecha la ventana. Por debajo de 768 px aparecen la barra
superior y el menú hamburguesa.

## Stack

| Pieza | Para qué |
|---|---|
| HTML5 | Un solo archivo, [`index.html`](index.html), semántico y en español |
| [Tailwind CSS v4](https://tailwindcss.com/) por CDN (`@tailwindcss/browser@4`) | Todo el estilo, solo con clases utility. El tema (colores y fuentes) va en un bloque `@theme` |
| [Charts.css](https://chartscss.org/) 1.2.0 por CDN | Los 3 gráficos, que son tablas HTML. Es la única excepción a "solo Tailwind" que permite el enunciado |
| Google Fonts | Geist y Geist Mono |

No hay CSS propio, ni atributos `style=""`, ni JavaScript propio, ni frameworks. El menú
hamburguesa funciona con `:target`, y los filtros de los rankings, con radios y las variantes
`has-checked:` y `group-has-[…]:` de Tailwind.

## Cómo cumple los criterios de evaluación

| Criterio | Cómo se cumple |
|---|---|
| **HTML semántico** | Enlace "Saltar al contenido", `aside` con `nav`, `header`, `main` con tres `section` (cada una con `aria-labelledby`), `article` por tarjeta y `footer`. Un `h1`, un `h2` por bloque y un `h3` por tarjeta, sin saltos. Las 7 tablas (incluidos los gráficos) tienen `caption` y `th` con `scope` |
| **Tailwind CSS** | Solo clases utility, sin CSS propio. Diseño mobile-first con los breakpoints `sm`, `md`, `lg`, `xl` y `2xl`, y maquetación con flex y grid |
| **Layout y componentes** | Los 3 bloques están separados: 5 KPIs, 5 drivers (embudo, plataformas, productos, engagement y actividad) y el detalle (alertas, 3 tablas y rankings con 4 filtros). Las tarjetas comparten la misma base de clases |
| **Diseño responsivo** | Funciona en móvil, tablet y escritorio sin scroll horizontal. En móvil hay barra superior y menú hamburguesa; desde 768 px, una barra lateral. Desde 1024 px las tablas caben enteras; por debajo, se desplazan dentro de su tarjeta y lo avisan |

Las comprobaciones y sus resultados están en [`verification.md`](verification.md).

### Sobre "el CSS con los estilos y las media queries"

El enunciado pide "solo Tailwind, sin CSS propio", pero en la entrega menciona "el CSS con los
estilos y las media queries". En este proyecto **no hay archivo CSS**: los estilos son las clases
de Tailwind y **las media queries son sus breakpoints** (`sm:`, `md:`, `lg:`, `xl:`), que Tailwind
convierte en media queries. Es la forma de cumplir las dos cosas a la vez.

## Estructura

```text
index.html             ← el dashboard
verification.md        ← comprobaciones de la entrega
BRIEFING.md            ← quién es la clienta y qué pide
CONTENT.md             ← todos los textos y las cifras
DESIGN.md              ← colores, tipografía, estructura y componentes
PLAN.md, plans/        ← plan de trabajo por fases
design/                ← maqueta aprobada y capturas de cada fase
AGENTS.md, .agents/, memory-bank/   ← reglas y contexto para agentes de IA
```

## Para trabajar en el repositorio

Tras clonarlo, activa el hook que impide subir secretos (usa [gitleaks](https://github.com/gitleaks/gitleaks)):

```bash
git config core.hooksPath .githooks
```
