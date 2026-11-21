# CONTENT — Textos y datos del dashboard de Lucía Vega

> Textos y cifras definitivos del dashboard, sacados de `BRIEFING.md`. Al construir la página se
> copian **tal cual**. Si un texto o una cifra no está aquí, se pregunta.
>
> Estado: **APROBADO** por Mateo el 20-11-2026.
>
> Todas las cifras son **datos de ejemplo** y cuadran entre sí: ventas × precio × 15 % =
> comisión, y la suma de cada tabla da el total del KPI. El aspecto visual va en `DESIGN.md`.

---

## 0. Datos de la página

| Campo | Texto |
|---|---|
| Título de la pestaña (`<title>`) | Panel de Lucía Vega · Octubre 2026 |
| Descripción (`meta description`) | Resultados de octubre 2026 de @luvega.daily: comisiones, ventas, conversión y engagement en Instagram, TikTok y YouTube. |
| Idioma | Español (`lang="es"`) |
| Aviso de las tablas que se desplazan (solo por debajo de 1024 px) | Desliza para ver toda la tabla → |

**Formato de las cifras:** español. Punto para los miles (`1.180.000`), coma para los decimales
(`1,61 %`), espacio antes de `%` y de `€`. Los ROI se escriben `2,48×`.

---

## 1. Cabecera y navegación

- **Enlace para saltar el menú:** "Saltar al contenido"
- **Logo:** las iniciales **LV** y el nombre **Lucía Vega**
- **Usuario:** @luvega.daily
- **Saludo (`h1`):** Hola, Lucía
- **Subtítulo:** Así han ido tus redes en octubre de 2026
- **Periodo:** 1–31 oct 2026 · comparado con septiembre
- **Nombre accesible del menú:** "Secciones del panel"
- **Botón del menú en móvil** (junto al icono de tres rayas, oculto al lector de pantalla): Menú
- **Botón para cerrar el menú en móvil** (junto al icono ✕, oculto al lector de pantalla):
  - Texto visible: Cerrar
  - Lo que oye el lector de pantalla: "Cerrar menú"
- **Pie del menú en móvil:** ninguno. Mateo lo quitó el 21-11-2026: el menú solo lleva el logo,
  "Cerrar" y los 5 enlaces.
- **Enlaces del menú** (en móvil, con su número decorativo "01 /" … "05 /" delante):
  1. Resumen → `#resumen`
  2. Plataformas → `#plataformas`
  3. Productos → `#productos`
  4. Campañas → `#campanas`
  5. Alertas → `#alertas`

---

## 2. Bloque 1 · Resumen (KPIs)

- **Título de la sección (`h2`):** 01 · Resumen del mes

| KPI | Valor | Cambio vs septiembre | Detalle |
|---|---|---|---|
| Comisiones | 3.840 € | ▲ +12 % (sept: 3.430 €) | De 25.600 € vendidos |
| Ventas | 355 | ▲ +8 % (sept: 329) | Precio medio 72,11 € |
| Conversión (clic → venta) | 1,61 % | ▼ −0,2 pp (sept: 1,81 %) | 22.050 clics |
| Engagement | 6,9 % | ▲ +0,5 pp (sept: 6,4 %) | 81.970 interacciones |
| Retorno (ROI) | 2,48× | ▲ +0,18 (sept: 2,30×) | 3.840 € / 1.550 € de costes |

**Glosario** (para textos de ayuda):
- **Comisión:** 15 % del precio de cada venta.
- **Conversión:** ventas / clics. **Conversión sobre alcance:** ventas / alcance.
- **Engagement:** interacciones / alcance.
- **ROI (retorno):** comisiones / costes (producción y promoción).

---

## 3. Bloque 2 · Drivers

- **Título de la sección (`h2`):** 02 · Qué explica el resultado

### 3.1 Embudo de ventas

- **Título:** Embudo de ventas
- **Subtítulo:** De las personas que te ven a las que compran
- **Nota (debajo de las cifras):** Barras en escala orientativa, no proporcional

| Paso | Valor | Paso al siguiente |
|---|---|---|
| Alcance | 1.180.000 | 6,9 % interactúa |
| Interacciones | 81.970 | 26,9 % hace clic |
| Clics al enlace | 22.050 | 1,61 % compra |
| Ventas | 355 | — |

### 3.2 Rendimiento por plataforma

- **Título:** Rendimiento por plataforma
- **Subtítulo:** Comisiones y retorno de cada red

| Plataforma | Comisiones | Costes | ROI |
|---|---|---|---|
| Instagram | 1.779 € | 600 € | 2,97× |
| TikTok | 1.123,50 € | 450 € | 2,50× |
| YouTube | 937,50 € | 500 € | 1,88× |
| **Total** | **3.840 €** | **1.550 €** | **2,48×** |

### 3.3 Rendimiento por producto

- **Título:** Rendimiento por producto
- **Subtítulo:** Qué producto te hace ganar más

| Producto | Precio | Ventas | Facturación | Comisión | Engagement |
|---|---|---|---|---|---|
| Producto A | 50 € | 180 | 9.000 € | 1.350 € | 7,4 % |
| Producto B | 120 € | 65 | 7.800 € | 1.170 € | 5,1 % |
| Producto C | 80 € | 110 | 8.800 € | 1.320 € | 7,8 % |

### 3.4 Actividad

- **Título:** Actividad del mes
- **Subtítulo:** Lo que has publicado en cada red

| Plataforma | Publicaciones |
|---|---|
| Instagram | 12 posts · 40 stories · 8 reels |
| TikTok | 22 vídeos |
| YouTube | 4 vídeos · 6 shorts |

### 3.5 Engagement por plataforma

- **Título:** Engagement por plataforma
- **Subtítulo:** Cómo responde tu comunidad

| Plataforma | Me gusta | Comentarios | Compartidos | Guardados | Total | Engagement |
|---|---|---|---|---|---|---|
| Instagram | 19.800 | 1.900 | 1.500 | 2.000 | 25.200 | 6,0 % |
| TikTok | 41.000 | 3.520 | 4.100 | 1.400 | 50.020 | 8,2 % |
| YouTube | 5.500 | 820 | 280 | 150 | 6.750 | 4,5 % |

---

## 4. Bloque 3 · Detalle operativo

- **Título de la sección (`h2`):** 03 · El detalle

### 4.1 Tabla de plataformas

- **Título:** Plataformas
- **Pie de tabla:** ★ = mejor plataforma en esa métrica

| Plataforma | Alcance | Engagement | Clics | CTR | Ventas | Conversión | Conv. / alcance | Comisión | ROI |
|---|---|---|---|---|---|---|---|---|---|
| Instagram | 420.000 | 6,0 % | 8.400 | 2,0 % | 168 | 2,00 % ★ | 0,040 % | 1.779 € ★ | 2,97× ★ |
| TikTok | 610.000 ★ | 8,2 % ★ | 9.150 | 1,5 % | 112 | 1,22 % | 0,018 % | 1.123,50 € | 2,50× |
| YouTube | 150.000 | 4,5 % | 4.500 | 3,0 % ★ | 75 | 1,67 % | 0,050 % ★ | 937,50 € | 1,88× |

### 4.2 Tabla de productos

- **Título:** Productos

| Producto | Precio | Ventas (IG / TikTok / YT) | Comisión | Costes | ROI |
|---|---|---|---|---|---|
| Producto A | 50 € | 180 (90 / 65 / 25) | 1.350 € | 500 € | 2,70× |
| Producto B | 120 € | 65 (28 / 12 / 25) | 1.170 € | 550 € | 2,13× |
| Producto C | 80 € | 110 (50 / 35 / 25) | 1.320 € | 500 € | 2,64× |

### 4.3 Tabla de campañas

- **Título:** Campañas de octubre
- **Pie de tabla:** Las 135 ventas restantes llegaron fuera de campaña.

| Campaña | Fechas | Producto | Plataformas | Ventas / objetivo | Comisión | Estado |
|---|---|---|---|---|---|---|
| Rutina de otoño | 1–15 oct | A | Instagram, TikTok | 110 / 100 | 825 € | Superada |
| Reto 7 días | 10–24 oct | C | TikTok, Instagram | 60 / 50 | 720 € | Superada |
| Unboxing B | 3–20 oct | B | YouTube | 25 / 40 | 450 € | Por debajo |
| Preventa Black Friday | 25–31 oct | C | Instagram | 25 / 30 | 300 € | Casi |

### 4.4 Alertas

- **Título:** Alertas

| Tipo | Texto |
|---|---|
| Caída | **Conversión en YouTube −0,6 pp.** Baja al 1,67 % durante "Unboxing B". |
| Pico | **14 ventas en un día en TikTok.** El 12 de octubre, con "Reto 7 días" (la media es de 3,6). |
| Anomalía | **Stories de Instagram con CTR del 0,8 %.** El resto de tu contenido en Instagram está en el 2,3 %. |

### 4.5 Rankings (listados con filtros)

- **Título:** Rankings
- **Nombre accesible del grupo de filtros:** "Elegir ranking"
- **Filtros:** Top productos · Top plataformas · Top campañas · Oportunidades

| Filtro | 1 | 2 | 3 |
|---|---|---|---|
| Top productos (por comisión) | Producto A · 1.350 € | Producto C · 1.320 € | Producto B · 1.170 € |
| Top plataformas (por ROI) | Instagram · 2,97× | TikTok · 2,50× | YouTube · 1,88× |
| Top campañas (por ventas) | Rutina de otoño · 110 | Reto 7 días · 60 | Unboxing B · 25 |
| Oportunidades | **Más Producto B en YouTube:** es el de precio más alto y YouTube tiene el mejor CTR (3,0 %). | **Revisa las stories de Instagram:** su CTR (0,8 %) está muy por debajo de tu media. | **Lleva el engagement de TikTok a ventas:** tiene el mejor engagement (8,2 %) pero la conversión más baja (1,22 %). |

---

## 5. Pie

- Datos de ejemplo · Proyecto de 4Geeks Academy
