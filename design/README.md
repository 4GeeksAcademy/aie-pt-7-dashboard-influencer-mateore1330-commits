# design/ — Maqueta aprobada (solo referencia)

Código de las tres mesas de la "propuesta 2b · Studio claro morado", aprobada por Mateo el
20-11-2026. Se hizo en el lienzo de diseño de Claude
(https://claude.ai/artifact/TAENwNd12tfrvyC7PzMYhN, privado).

| Archivo | Mesa del lienzo | Qué muestra |
|---|---|---|
| `mockup-2b-escritorio.dc.html` | Propuesta 2b · Studio claro morado (elegida) | El dashboard completo a 1440 px, con sidebar |
| `mockup-2b-movil.dc.html` | 2b · Móvil (pulsa Menú) | Móvil a 390 px: barra superior con "Menú" y los primeros bloques |
| `mockup-2b-menu-abierto.dc.html` | 2b · Móvil, menú abierto | El menú hamburguesa abierto a pantalla completa |

## Cómo usarla

- **Manda `DESIGN.md`.** La maqueta sirve para copiar proporciones, espaciados y el aspecto
  general. Si algo no coincide con `DESIGN.md`, vale `DESIGN.md`. Ejemplos de diferencias ya
  decididas:
  - La sidebar aparece desde `md` (768 px), no solo en escritorio.
  - La franja de KPIs cambia de forma según el breakpoint (`DESIGN.md` §5).
  - Los gráficos finales se hacen con Charts.css, no con `div` (`DESIGN.md` §8).
- **Los textos y las cifras salen de `CONTENT.md`**, no de la maqueta. Por ejemplo, la maqueta
  pone "vs septiembre" en la etiqueta del periodo; el texto bueno es el de `CONTENT.md`.
- **No se publica ni se abre como web:** no funciona fuera del lienzo. Usa un formato propio
  (`<x-dc>`, `<helmet>`, `<sc-for>`, `{{…}}`, `data-props`, `support.js` y estilos en línea)
  que no forma parte de la web final. La web se escribe desde cero con HTML y clases de
  Tailwind.
- En la maqueta, el menú se abre con un pequeño script del lienzo. En la web final se hace sin
  JavaScript, con `:target` (`DESIGN.md` §7).
- `mockup-2b-menu-abierto.dc.html` importa la mesa del móvil por su nombre en el lienzo
  (`StudioClaroMovil`). Aquí ese archivo se llama `mockup-2b-movil.dc.html`.
