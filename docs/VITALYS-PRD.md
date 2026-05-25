# VITALYS — Product Requirements Document

> Versión 1.0 · 2026-05-25 · Idioma de la tienda: Español

---

## 1. Visión del producto

VITALYS es una tienda Shopify de suplementos premium de formulación europea. No compite en precio: compite en transparencia, rigor científico y confianza. La tienda debe transmitir la misma sensación que entrar en una farmacia de alto nivel en Zúrich — orden, claridad, autoridad contenida — sin caer nunca en el hype del mundo fitness.

**Público objetivo:** Profesionales de 28–45 años que toman sus decisiones de salud con la misma exigencia que aplican al resto de su vida. Conocen la diferencia entre óxido de magnesio y bisglicinato. Buscan datos, no promesas.

**Tagline:** *"La diferencia está en lo que no se ve."*

**Propuesta de valor en una frase:** Formulación europea sin concesiones, para quienes saben la diferencia.

---

## 2. Stack técnico

| Capa | Tecnología |
|------|-----------|
| Plataforma | Shopify (plan Basic o superior) |
| Tema base | **Dawn** — tema oficial Shopify, limpio, accesible, bien mantenido |
| Lenguaje de plantillas | Shopify Liquid + JSON templates |
| CSS | Personalización via `assets/vitalys.css` (tokens + utilidades de marca) |
| Tipografía | Google Fonts via Shopify font picker: Playfair Display + DM Sans |
| Control de versiones | **GitHub** — repositorio privado, rama `main` como producción |
| Despliegue | Shopify CLI (`shopify theme push`) o GitHub Actions con Shopify Theme Action |
| Editor de código | Claude Code — implementación y mantenimiento |

### Estructura de archivos clave

```
shopify-vitalys/
├── assets/
│   └── vitalys.css          # Tokens CSS de marca + clases utilitarias
├── config/
│   └── settings_data.json   # Paleta, tipografía, radios — configuración del tema
├── layout/
│   └── theme.liquid         # Layout global — importa vitalys.css
├── sections/                # Secciones Liquid del tema Dawn
├── templates/
│   ├── index.json           # Homepage — 7 secciones
│   └── product.json         # Página de producto — 3 secciones principales
└── VITALYS-brand.md         # Documento de identidad de marca (fuente de verdad)
```

---

## 3. Sistema de diseño

### 3.1 Paleta de colores

| Token CSS | Nombre | Hex | Uso |
|-----------|--------|-----|-----|
| `--vitalys-cream` | Cream | `#F7F5F0` | Fondo principal, secciones limpias, fondo de producto |
| `--vitalys-carbon` | Carbon | `#1C1C1A` | Texto principal, navbar, botones CTA primarios |
| `--vitalys-gold` | Gold | `#C8A96E` | Acento premium, badges, subrayados, detalles |
| `--vitalys-sand` | Sand | `#E8E3D9` | Fondos secundarios, tarjetas, separadores |
| `--vitalys-forest` | Forest | `#3D5A48` | Badges orgánicos/naturales, ingredientes |

**Reglas de uso:**
- Cream + Carbon es la combinación base. Nunca mezcles Gold con Forest directamente.
- Gold solo aparece como acento — nunca como fondo en bloques grandes.
- Botones primarios: fondo Carbon, texto Cream.
- Botones secundarios: borde Carbon, fondo transparente, texto Carbon.
- Texto sobre Forest: siempre Cream.

**Mapeo de color schemes en Shopify (`settings_data.json`):**

| Scheme | Nombre interno | Background | Texto | Botones |
|--------|---------------|------------|-------|---------|
| scheme-1 | Cream | `#F7F5F0` | `#1C1C1A` | Carbon CTA |
| scheme-2 | Sand | `#E8E3D9` | `#1C1C1A` | Carbon CTA |
| scheme-3 | Forest | `#3D5A48` | `#F7F5F0` | Cream CTA |
| scheme-4 | Gold | `#C8A96E` | `#1C1C1A` | Carbon CTA |
| scheme-5 | Carbon | `#1C1C1A` | `#F7F5F0` | Gold CTA (`#C8A96E`) |
| scheme-6 | Transparent/Hero | transparente | `#F7F5F0` | Cream CTA |

---

### 3.2 Tipografía

#### Display — Headlines y títulos
**Playfair Display** · Google Fonts · Peso 400 / 500

```
Uso: H1, H2, citas de marca, tagline, nombres de producto
Tamaño desktop: H1 88px · H2 56px · H3 40px
Tamaño mobile: H1 40px · H2 32px · H3 24px
Estilo: normal o itálica para énfasis emocional
Letter-spacing: -0.03em en tamaños grandes (override en vitalys.css)
Line-height: 1.1–1.2
```

#### Body — Texto corrido e interfaz
**DM Sans** · Google Fonts · Peso 400 / 500

```
Uso: párrafos, descripciones, navegación, etiquetas, botones
Tamaño base: 16px
Tamaño metadatos: 12px
Letter-spacing: 0 en texto normal · +0.15em en uppercase labels
Line-height: 1.6 en párrafos · 1.2 en UI elements
```

#### Jerarquía tipográfica

| Nivel | Fuente | Peso | Tamaño desktop | Uso |
|-------|--------|------|----------------|-----|
| H1 | Playfair Display | 500 | 88px | Hero headlines |
| H2 | Playfair Display | 400 | 56px | Titulos de sección |
| H3 | Playfair Display | 400 | 40px | Subtítulos, nombres de producto |
| H4 | DM Sans | 500 | 20px | Subencabezados de interfaz |
| Body | DM Sans | 400 | 16px | Texto corrido |
| Label | DM Sans | 500 | 11–12px | Uppercase, letter-spacing +0.15em |
| Caption | DM Sans | 400 | 12px | Metadatos, fechas, notas |

---

### 3.3 Espaciado y layout

```
Ancho máximo de contenedor: 1280px
Padding lateral (desktop): 48px
Padding lateral (mobile): 20px
Gap entre secciones: 80px desktop · 48px mobile
Gap entre columnas de cards: 24px desktop · 16px mobile
Border-radius general: 4px (botones, badges, inputs, cards)
```

---

### 3.4 Botones

**Primario (Carbon)**
```css
background: #1C1C1A;
color: #F7F5F0;
border-radius: 4px;
padding: 14px 28px;
font-family: DM Sans, 500;
font-size: 14px;
letter-spacing: 0.05em;
text-transform: uppercase;
```

**Secundario (outline)**
```css
background: transparent;
color: #1C1C1A;
border: 1.5px solid #1C1C1A;
border-radius: 4px;
padding: 13px 27px; /* 1px menos para compensar el borde */
```

**CTA sobre fondo oscuro (Gold)**
```css
background: #C8A96E;
color: #1C1C1A;
border-radius: 4px;
```

**Estados:**
- Hover en primario: `opacity: 0.85` — sin cambio de color
- Hover en outline: `background: rgba(28, 28, 26, 0.06)`
- Focus: outline 2px offset 2px en Gold

---

### 3.5 Estilo de imágenes

**Imágenes de producto:**
- Fondo siempre Cream (`#F7F5F0`) — sin sombras, sin gradientes
- Mínimo 4 ángulos: frontal, reverso, detalle ingredientes, lifestyle
- Formato cuadrado 1:1 o ligeramente vertical 4:5
- Sin props ni accesorios ajenos al producto

**Imágenes lifestyle:**
- Personas reales, luz natural cálida, tonos neutros
- Entornos: cocina minimalista, escritorio ordenado, exteriores luz natural
- Sin gimnasios, sin pesas, sin estética "gym rat"
- Diversidad de edad visible (target 28–45, no solo 25)

**Iconografía:**
- Línea fina (1.5–2px stroke), sin relleno
- Color Carbon sobre fondos claros · Cream sobre fondos oscuros
- Tamaño estándar: 20–24px en interfaz, 32–40px en secciones editoriales

---

### 3.6 Badges y etiquetas

```css
/* Badge Gold — acento premium */
.vitalys-badge-gold {
  background: #C8A96E;
  color: #1C1C1A;
  font: 500 11px/1 "DM Sans";
  letter-spacing: 0.15em;
  text-transform: uppercase;
  padding: 3px 10px;
  border-radius: 4px;
}

/* Badge Forest — certificación / origen natural */
.vitalys-badge-forest {
  background: #3D5A48;
  color: #F7F5F0;
  /* mismas reglas */
}
```

Valores de badge: `BESTSELLER` · `NUEVO` · `PACK` · `EUROPEO` · `GMP`

---

## 4. Homepage — 7 secciones

### Sección 01 — Hero

**Scheme:** scheme-1 (Cream) · **Altura:** large (viewport completo en desktop)

**Descripción visual:**
Imagen del producto principal a la derecha, ocupando el 55% del ancho. A la izquierda, sobre fondo Cream: el headline en Playfair Display a 88px, el tagline o un subheadline en DM Sans 18px y un único botón CTA en Carbon. Sin sliders. Sin vídeo autoplay. Sin contador de descuento.

**Copy:**
```
[H1] La diferencia está en lo que no se ve.
[Sub] Suplementos formulados con ingredientes europeos certificados
       y dosificación clínica exacta.
[CTA] Descubrir productos →
```

**Reglas:**
- Un solo CTA. Sin secundario.
- No mostrar precio en el hero.
- Imagen sin sombras, fondo Cream.

---

### Sección 02 — Barra de confianza (Marquee)

**Scheme:** scheme-2 (Sand) · **Altura:** 48–56px

**Descripción visual:**
Fila horizontal con scroll continuo (marquee loop). Texto en DM Sans 12px, uppercase, letter-spacing +0.15em. Separadores en Gold (·). Velocidad lenta, sin interacción.

**Copy:**
```
Fabricado en Europa · Fórmula clínica · Sin dióxido de titanio · Nutricionistas propios · +4.800 valoraciones · Fabricado en Europa · ...
```

---

### Sección 03 — Categorías por objetivo

**Scheme:** scheme-1 (Cream)

**Descripción visual:**
Grid de 3 columnas en desktop (2 en mobile). Cada tarjeta: imagen lifestyle cuadrada, etiqueta de categoría en uppercase (DM Sans 11px, letter-spacing), y un hover sutil (ligero oscurecimiento de la imagen). Sin precios, sin botones de añadir al carrito — es navegación, no conversión.

**Encabezado:** H2 Playfair "¿Cuál es tu objetivo?"

**Categorías (6):**
1. Sueño y descanso
2. Energía y foco
3. Rendimiento
4. Salud digestiva
5. Estrés
6. Piel y cabello

---

### Sección 04 — Bestsellers

**Scheme:** scheme-1 (Cream)

**Descripción visual:**
Fila de 4 producto-cards en desktop (scroll horizontal en mobile). Cada card:
- Imagen cuadrada sobre fondo Cream
- Nombre en Playfair 18px
- 2–3 pills de beneficio (DM Sans 11px, outline Carbon)
- Precio en DM Sans 500
- Botón pequeño: "Añadir al carrito" — Carbon, ancho completo de la card

**Encabezado:** H2 Playfair "Los más vendidos"

**Filtros opcionales:** tabs sutiles — Más vendidos / Nuevos / Packs

---

### Sección 05 — Por qué VITALYS (4 pilares)

**Scheme:** scheme-2 (Sand)

**Descripción visual:**
4 columnas en desktop, 2 en tablet, 1 en mobile. Cada columna:
- Icono de línea fina (24px) alineado a la izquierda
- Título H4 DM Sans 500
- Texto de 2 líneas máximo, DM Sans 400 14px, color Carbon 75% opacidad

Sin decoraciones extra. Sin flechas, sin fondos por columna. La arquitectura limpia ES el mensaje.

**Encabezado:** H2 Playfair "Por qué VITALYS"

**Los 4 pilares:**
| Icono | Título | Texto |
|-------|--------|-------|
| Hoja | Ingredientes europeos certificados | Trazabilidad completa. Sin materias primas de origen dudoso. |
| Microscopio | Dosificación clínica exacta | Las cantidades que usan los estudios, no las que abaratan el producto. |
| Documento | Fórmulas propias | Sin copiar. Sin fórmulas propietarias que oculten cantidades. |
| Check | Packaging sin rellenos | Sin dióxido de titanio ni excipientes innecesarios. |

---

### Sección 06 — Transparencia de fórmula

**Scheme:** scheme-5 (Carbon — fondo oscuro)

**Descripción visual:**
Layout de dos columnas: izquierda imagen del ingrediente o packaging con detalle, derecha texto editorial. Texto en Cream sobre Carbon. El ingrediente destacado lleva la clase `.vitalys-ingredient-highlight`: borde izquierdo en Gold, nombre en Playfair, dosis en Gold, explicación en Cream 75% opacidad.

**Copy:**
```
[H2] Cada miligramo tiene un motivo.
[Ingrediente destacado]
  Magnesio bisglicinato · 300 mg por dosis
  Absorción 4× superior al óxido de magnesio
[CTA] Ver todos los ingredientes →
```

---

### Sección 07 — Quiz diagnóstico (CTA secundario)

**Scheme:** scheme-1 (Cream)

**Descripción visual:**
Centrado, sin imagen. Headline Playfair. Subheadline DM Sans. Botón outline Carbon. Colocado en la parte baja de la homepage, como invitación tranquila — no como popup agresivo.

**Copy:**
```
[H2] ¿No sabes por dónde empezar?
[Sub] Responde 3 preguntas y te recomendamos el suplemento ideal para ti.
[CTA] Hacer el quiz
```

---

## 5. Página de producto — 3 secciones

### Sección A — `product-information` (Scheme: scheme-1)

Layout estándar galería izquierda / información derecha (desktop). Stack vertical en mobile.

**Bloque de galería:**
- Mínimo 4 imágenes: frontal, reverso, detalle, lifestyle
- Fondo Cream en todas las imágenes
- Thumbnails debajo en desktop, swipe en mobile
- Sin zoom agresivo — el producto es limpio, no hay nada que ocultar

**Bloque de título y precio:**
```
[badge si aplica: BESTSELLER · NUEVO]
[H1 Playfair] Magnesio Bisglicinato 300
[benefit line DM Sans 500 18px]
  Recuperación muscular y mejora de la calidad del sueño.
[precio DM Sans 500 24px]
  29,90 €
```
- Sin precio tachado a menos que haya descuento activo
- Benefit line antes del precio — primero el valor, luego el coste

**Bloque de variantes:**
- Selector de cantidad: limpio, sin flechas grandes
- Variantes de formato si aplica (60/120 cápsulas): radio buttons, no dropdown

**Bloque de compra:**
- Botón primario "Añadir al carrito" — Carbon, ancho completo en mobile
- Opción suscripción con descuento (15–20%): visible pero no más prominente que el botón principal
- Garantía bajo el botón: "Envío en 24h · Devolución gratuita 30 días"

**Fila de trust icons (4 iconos con texto breve):**
```
[icono] Fabricado en UE
[icono] Sin dióxido de titanio
[icono] Certificación GMP
[icono] Envío en 24h
```

**Descripción del producto:**
- Qué es (1 párrafo, máximo 4 líneas)
- Para quién (perfil específico)
- Qué lo diferencia

**Tabla de ingredientes:**
| Ingrediente | Forma química | Dosis/toma | % VRN |
|-------------|---------------|------------|-------|
Sin "blend", sin cantidades ocultas.

**Modo de uso:**
- Cuándo tomarlo · Cantidad exacta · Con qué combinarlo
- Un icono por punto

---

### Sección B — FAQ acordeón (Scheme: scheme-2 / Sand)

**Encabezado:** H2 Playfair "Preguntas frecuentes"

Acordeón de 5 preguntas. Animación de apertura sutil (height transition). El signo `+` → `−` al abrir. Tipografía body DM Sans en las respuestas.

**Preguntas predeterminadas:**
1. ¿Es apto para veganos?
2. ¿Puedo combinarlo con otros suplementos?
3. ¿Cuánto tiempo hasta notar efecto?
4. ¿Tiene alérgenos?
5. ¿Qué pasa si me lo salto un día?

**Regla de respuestas:** Directas. Sin "consulta a tu médico" como única respuesta. Sin evasivas.

---

### Sección C — Combina bien con (Scheme: scheme-1)

**Encabezado:** H3 Playfair "Combina bien con…"

Grid de 3 producto-cards. Cada recomendación va acompañada de una línea de justificación:
> *"Para potenciar la recuperación, añade Omega Elite a tu rutina."*

Nunca "También te puede gustar" sin contexto.

---

## 6. Navegación y header

**Layout:** Logo centrado (o izquierda), navegación principal en línea, iconos de búsqueda / cuenta / carrito a la derecha.

**Scheme:** Carbon (fondo `#1C1C1A`, texto Cream) en scroll / sticky. Fondo transparente en el hero.

**Menú principal:**
```
Productos  |  Por qué VITALYS  |  Ingredientes  |  Blog  |  [Buscar] [Cuenta] [Carrito]
```

**Comportamiento:**
- Sticky desde el primer scroll
- Sin mega-menu. Dropdown simple con las categorías de producto.
- Logo: tipografía únicamente (wordmark), sin símbolo complejo

---

## 7. Footer

**Scheme:** Carbon (fondo oscuro)

**Estructura 4 columnas:**
- Col 1: Logo + tagline + claim de 2 líneas
- Col 2: Productos (links a categorías)
- Col 3: Empresa (Quiénes somos, Ingredientes, Blog, Contacto)
- Col 4: Newsletter — "Sin spam. Solo ciencia." + input email

**Fila inferior:**
```
© 2026 VITALYS · Política de privacidad · Aviso legal · Cookies
```

Iconos de pago: mínimos, en Cream 50% opacidad.

---

## 8. Tono de comunicación

### VITALYS habla así

| Principio | Descripción |
|-----------|-------------|
| **Preciso y contenido** | Cada palabra tiene un motivo. Sin adornos innecesarios. |
| **Con autoridad, sin arrogancia** | Conoce el sector y no necesita demostrarlo en exceso. |
| **Honesto sobre lo que no es** | Admite limitaciones antes de que las pregunten. |
| **Sin emojis en web** | En RRSS, máximo 1 emoji funcional si aplica. |

### Ejemplos de copy CORRECTO

```
"Diseñado para las horas que realmente importan."
"Cada miligramo tiene un motivo."
"No añadimos lo que no aporta. Nunca."
"Fabricado en Europa bajo estándares GMP. Sin excepciones."
"El magnesio bisglicinato no es el más barato. Es el que mejor funciona."
"Formulación sin concesiones, para quienes saben la diferencia."
```

### VITALYS NUNCA dice

```
❌ "¡El suplemento más potente del mercado!"
❌ "Oferta limitada — ¡solo hoy!"
❌ "Resultados garantizados en 7 días."
❌ "Tu mejor versión empieza aquí 💪🔥"
❌ "Fórmula patentada exclusiva" (sin desglosar qué contiene)
❌ "Consulta a tu médico" como única respuesta a una pregunta concreta
```

### Voz del producto vs voz de la marca

**Voz del producto** (página de producto, tabla de ingredientes): técnica, exacta, sin florituras.
> *"Magnesio bisglicinato · 300 mg · Absorción 4× superior al óxido de magnesio"*

**Voz de marca** (hero, secciones editoriales, newsletter): contenida, filosófica, un punto poética.
> *"La diferencia está en lo que no se ve."*

---

## 9. Sensación general

La tienda debe sentirse como un objeto bien diseñado: **quieta, segura de sí misma, sin necesidad de convencer**. El visitante llega, lee, confía, compra. Sin urgencia artificial, sin banners rojos, sin contadores de stock falsos.

La referencia más cercana no es una tienda de suplementos. Es la landing de un estudio de arquitectura premium o una farmacia independiente europea: espacio en blanco generoso, tipografía con carácter, fotografía honesta.

Si en algún momento algo de la tienda suena a "oferta del día" o parece urgente sin serlo, está mal.

**El test rápido:** ¿Lo aprobaría una nutricionista clínica seria con diez años de experiencia? Si no, no va.

---

## 10. Checklist de implementación

### Fase 1 — Base de marca
- [x] Paleta de colores en `settings_data.json` (7 schemes)
- [x] Tipografía Playfair Display + DM Sans en `settings_data.json`
- [x] `assets/vitalys.css` con tokens CSS y clases utilitarias
- [x] `layout/theme.liquid` carga `vitalys.css`

### Fase 2 — Homepage
- [x] `templates/index.json` — 7 secciones con copy y schemes correctos
- [ ] Imágenes lifestyle cargadas en Shopify Admin
- [ ] Colecciones creadas y asignadas a la sección de categorías
- [ ] Marquee trust bar revisada en mobile

### Fase 3 — Página de producto
- [x] `templates/product.json` — FAQ acordeón + "Combina bien con…"
- [ ] Tabla de ingredientes en la descripción del producto (formato HTML)
- [ ] Trust icons con SVG reales
- [ ] Suscripción recurrente configurada (Shopify Subscriptions o app)

### Fase 4 — Navegación y global
- [ ] Header Carbon sticky configurado
- [ ] Menú con dropdown de categorías
- [ ] Footer 4 columnas con newsletter
- [ ] Favicon y social sharing image (1200×630, Carbon + wordmark)

### Fase 5 — SEO y rendimiento
- [ ] Meta titles y descriptions por plantilla
- [ ] `alt` en todas las imágenes de producto
- [ ] Structured data (Product schema) en páginas de producto
- [ ] Core Web Vitals — LCP < 2.5s, CLS < 0.1

### Fase 6 — Contenido
- [ ] 8–12 productos creados con tabla de ingredientes completa
- [ ] Página "Ingredientes" con el glosario de formas químicas
- [ ] Quiz de 3 pasos configurado
- [ ] 2–3 artículos de blog iniciales

---

## 11. Referencias y fuentes de verdad

| Recurso | Ubicación |
|---------|-----------|
| Documento de marca VITALYS | `VITALYS-brand.md` |
| Tokens CSS de marca | `assets/vitalys.css` |
| Configuración de tema | `config/settings_data.json` |
| Referencia visual de mercado | belevels.com |
| Especificaciones de componentes | Este documento (secciones 3–6) |

---

*PRD generado: 2026-05-25 · Marca validada · Stack definido · Listo para construcción con Claude Code.*
