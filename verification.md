# Verificación — Dashboard de Lucía Vega

> Comprobación final de la entrega (fase 5, [`plans/phase-5-verification.md`](plans/phase-5-verification.md)),
> hecha el 22-11-2026 sobre la rama `chore/phase-5-verification`. Comprueba los 4 criterios de
> evaluación y los criterios globales de [`PLAN.md`](PLAN.md) §5.

## Resumen

| # | Comprobación | Resultado | Corrección |
|---|---|---|---|
| 1 | HTML válido | ✅ | — |
| 2 | Semántica y jerarquía | ✅ | — |
| 3 | Solo Tailwind | ✅ | — |
| 4 | Colores del tema | ✅ | — |
| 5 | Mínimos del enunciado | ✅ | — |
| 6 | Responsivo | ✅ | — |
| 7 | Menú y filtros | ✅ | `f5e5095` |
| 8 | Accesibilidad | ✅ | `7293c1d` |
| 9 | Textos y cifras | ✅ | `d6521bc` |
| 10 | Revisión de código | ✅ | `f5e5095`, `baa4c41`, `586580d` |

## Detalle

### 1. HTML válido

**Herramienta:** validador Nu de W3C (https://validator.w3.org/nu/), enviando `index.html`.

| Archivo validado | Errores | Avisos |
|---|---|---|
| `index.html` completo | 2 | 0 |
| `index.html` sin el bloque `<style type="text/tailwindcss">` | 0 | 0 |

Los 2 errores son los del bloque de tema que exige Tailwind v4 por CDN. Mateo los aceptó el
20-11-2026 ([`PLAN.md`](PLAN.md) §5, regla HT-02):

- *The only allowed value for the "type" attribute for the "style" element is "text/css"* (línea 13).
- *CSS: Unrecognized at-rule "@theme"* (línea 14).

### 2. Semántica y jerarquía

- **Landmarks:**
  - "Saltar al contenido" → `aside` con `nav` → `header` (barra del móvil, con el panel del menú y
    su `nav`) → `main` → `footer`.
  - Dentro del `main`, 3 `section`, todas con `aria-labelledby`, y 14 `article`.
- **Títulos:** 1 `h1`, 3 `h2` y 16 `h3`, sin saltos:

  ```text
  h1 Hola, Lucía
    h2 01 · Resumen del mes
      h3 Comisiones · Ventas · Conversión (clic → venta) · Engagement · Retorno (ROI)
    h2 02 · Qué explica el resultado
      h3 Embudo de ventas · Rendimiento por plataforma · Rendimiento por producto · Engagement por plataforma · Actividad del mes
    h2 03 · El detalle
      h3 Alertas · Plataformas · Campañas de octubre · Productos · Rankings
  ```

- **Tablas:** 7 tablas (3 gráficos de Charts.css y 4 de datos) con 7 `caption`; 58 `th`, todos
  con `scope`.
- **Anclas:** los destinos de los 8 enlaces internos existen: `contenido`, `cabecera`, `menu`,
  `resumen`, `plataformas`, `productos`, `campanas` y `alertas`.

### 3. Solo Tailwind

| Búsqueda | Resultado |
|---|---|
| `style="` | 0 |
| `<style>` | 1, el de `@theme`, que solo contiene `--font-*` y `--color-*` |
| `<script>` | 1, el CDN `@tailwindcss/browser@4` |
| `on*=` y `javascript:` | 0 |
| Archivos `.css` o `.js` propios | 0 |
| `cdn.tailwindcss.com`, `tailwind.config`, `@tailwind`, `@apply`, `@layer`, `@config` | 0 |
| Breakpoints en uso | `sm` (20), `md` (32), `lg` (20), `xl` (32), `2xl` (5) |

La única excepción es Charts.css 1.2.0 por CDN, que permite el enunciado. Hay un solo modificador
`!` (`[&_tr]:bg-lavanda-50!`), justificado en la regla CH-02: Charts.css va sin capa y gana a las
utilidades de Tailwind.

### 4. Colores del tema

| Búsqueda | Resultado |
|---|---|
| Colores de la paleta por defecto de Tailwind (`purple-`, `gray-`…) | 0 |
| Colores arbitrarios (`[#…]`, `[rgb…]`…) | 0 |
| `text-rosa-500` (contraste 3,16:1, prohibido como texto) | 0 |

Todos los colores salen de los 24 de `DESIGN.md` §2, más `white`.

### 5. Mínimos del enunciado

| Mínimo | Hay |
|---|---|
| Al menos 3 KPIs | 5: comisiones, ventas, conversión, engagement y ROI |
| Al menos 3 drivers | 5: embudo, plataformas, productos, engagement y actividad |
| Tablas o listados de detalle | 3 tablas (plataformas, campañas y productos), 3 alertas y 4 rankings con filtros |

### 6. Responsivo

**Herramienta:** Playwright (Chromium).

| Ancho | Scroll horizontal de la página | Navegación | Tablas |
|---|---|---|---|
| 375 px | No | Barra superior con "Menú" | Se desplazan, con aviso y degradado |
| 768 px | No | Barra lateral | Se desplazan, con aviso y degradado |
| 1024 px | No | Barra lateral | Caben enteras |
| 1440 px | No | Barra lateral | Caben enteras |

Capturas de página completa en [`design/screenshots/fase-5/`](design/screenshots/fase-5/):
`375.png`, `768.png`, `1024.png` y `1440.png`. Durante la fase 4 también se comprobó que no hay
scroll horizontal a 640, 900, 1023, 1100, 1279, 1280 y 1728 px, ni con zoom al 200 %.

### 7. Menú y filtros

**Herramienta:** Playwright, con ratón y teclado reales.

| Prueba | Resultado |
|---|---|
| Abrir el menú a 375 px | ✅ la página no se mueve |
| Rueda del ratón con el menú abierto | ✅ la página no hace scroll |
| "Cerrar" | ✅ cierra y deja la página donde estaba |
| "Campañas" desde el menú | ✅ lleva a la tabla (el título queda por debajo de la barra) y cierra el menú |
| Tabulador con el menú abierto | ✅ no sale del panel (Cerrar → 5 enlaces → Cerrar) |
| 1440 px con `#menu` en la dirección | ✅ el panel no se ve, la página sí, hay scroll y "Saltar al contenido" funciona (corregido en `f5e5095`) |
| Filtros con ratón | ✅ cada uno muestra solo su lista; al cargar, "Top productos" |
| Filtros con teclado (flechas) | ✅ igual, con el foco visible en el `<label>` |

### 8. Accesibilidad

| Prueba | Resultado |
|---|---|
| **Lighthouse** (Mateo, Brave, modo Navegación, móvil) | ✅ 100 en todas las categorías analizadas |
| **axe-core 4.10** (WCAG 2.0, 2.1 y 2.2 A/AA y buenas prácticas) a 1440 px, con los filtros cambiados | ✅ 0 problemas |
| **axe-core** a 375 px, con el menú cerrado y abierto | ✅ 0 problemas (antes de `7293c1d`, 1 grave: `scrollable-region-focusable`) |
| **Contraste** (fórmula WCAG, todo el texto visible) | ✅ mínimo 5,05:1 (`rosa-700` sobre `rosa-50`) |
| **Zonas táctiles** | ✅ ninguna por debajo de 44 px; los enlaces del menú miden 60 px |
| **Teclado** | ✅ recorrido completo a 375 y 1440 px, con orden lógico y foco visible en todo |
| **Movimiento** | ✅ no hay animaciones ni transiciones |
| **VoiceOver** | ➖ No se hizo (decisión de Mateo) |

Lo corregido:

- **`7293c1d`:** las 4 cajas con scroll de las tablas no se podían usar con el teclado en Safari
  ni en Firefox. Ahora llevan `role="region"`, un nombre (`aria-labelledby`, el título de su
  tarjeta) y `tabindex="0"`. Desde 1024 px, donde las tablas caben, siguen siendo una parada del
  tabulador. Es un coste aceptado: quitarla según el ancho exigiría JavaScript.

Lo revisado que no es un problema:

- **54 contrastes "sin decidir" de axe a 375 px:** son celdas de tabla que quedan fuera de la
  parte visible de su caja o bajo el degradado, y axe no puede leer su fondo. Tienen el mismo color
  que el resto de la tabla (`tinta` sobre `superficie`, 16,86:1).

Lo que se acepta perder con el menú sin JavaScript (`DESIGN.md` §7, regla A11Y-05):

- El lector dice "enlace" y no "botón, expandido".
- Esc no cierra el menú.
- La dirección muestra `#menu`.

### 9. Textos y cifras

**Herramienta:** script que extrae los 235 textos visibles y `aria-label` de `index.html` y los
busca en [`CONTENT.md`](CONTENT.md).

Todos son literales, con estas excepciones permitidas:

- **"01 /" … "05 /":** los números decorativos del menú, de `CONTENT.md` §1.
- **"▼ Caída", "▲ Pico" y "◆ Anomalía":** el tipo de alerta de `CONTENT.md` §4.4 con su símbolo,
  de `DESIGN.md` §6.
- **"ROI 2,50×" y "ROI 1,88×":** la cifra de cada barra, según la regla escrita en `CONTENT.md`
  §3.2.

En esta fase se añadieron a `CONTENT.md` §3.2 tres textos de la tarjeta de plataformas que estaban
montados con sus cifras (`d6521bc`, decisión de Mateo):

- "Comisiones · ROI".
- "Costes: Instagram 600 € · TikTok 450 € · YouTube 500 € · Total 1.550 €".
- "Total: 3.840 € · ROI 2,48×".

### 10. Revisión de código

**Herramienta:** la agente Claudia, con la skill `rx-review`. Revisó todo el repositorio, con el
foco en `index.html`.

- **Veredicto:** listo con cambios menores. Nada bloqueante ni importante.
- **Secretos:** gitleaks sin fugas en los archivos ni en todo el historial. Los correos de los
  commits son `noreply`. `.env` está ignorado y el hook está activo.
- **Reglas:** se cumplen HT-01 a HT-06, TW-01 a TW-07, CH-01 a CH-04 y A11Y-01 a A11Y-06. No hay
  IDs duplicados, etiquetas sin cerrar ni referencias rotas.

Hallazgos menores y qué se hizo:

| Hallazgo | Qué se hizo |
|---|---|
| 3 textos de la tarjeta de plataformas sin estar literales en `CONTENT.md` | Añadidos a `CONTENT.md` §3.2 (`d6521bc`) |
| "Saltar al contenido" quedaba `invisible` en escritorio con `#menu` en la dirección | `md:[body:has(#menu:target)_&]:visible` (`f5e5095`) |
| Reglas A11Y-03 y A11Y-05 y `architecture.md` desfasadas | Actualizadas (`baa4c41`) |
| Vista previa abierta a toda la red local; `server.py` con `debug=True` | El comando usa `--bind 127.0.0.1` (`baa4c41`) y `server.py` se borró (`586580d`), por decisión de Mateo |

## Entrega

- **README:** [`README.md`](README.md) es nuevo, en español. Explica qué es, cómo verlo, el
  stack, cómo cumple cada criterio y la contradicción del enunciado sobre "el CSS y las media
  queries". Se borraron `README.es.md` y `README.cn.md` de la plantilla.
- **Publicación:** la web no se publica en GitHub Pages (decisión de Mateo). Se entrega la URL del
  repositorio.
