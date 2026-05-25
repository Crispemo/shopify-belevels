# VITALYS Brand Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Aplicar la identidad de marca VITALYS (colores, tipografía, estructura homepage y producto) al tema Shopify Horizon del proyecto shopify-belevels.

**Architecture:** Los colores y fuentes se controlan desde `config/settings_data.json`. Los tokens de marca Gold/Forest se inyectan como CSS custom properties en `assets/vitalys.css`. La estructura de páginas se define en los JSON de templates.

**Tech Stack:** Shopify Horizon theme · Liquid · JSON templates · CSS custom properties

---

## Mapa de archivos

| Archivo | Qué cambia |
|--------|-----------|
| `config/settings_data.json` | Esquemas de color + tipografía (fuentes, tamaños, border-radius) |
| `assets/vitalys.css` | NUEVO — CSS custom properties de marca (Gold, Forest, acento) |
| `layout/theme.liquid` | Añadir `<link>` a vitalys.css |
| `templates/index.json` | Homepage VITALYS — 8 secciones |
| `templates/product.json` | Página de producto — 10 bloques |

---

## Task 1: Paleta VITALYS en color_schemes

**Files:**
- Modify: `config/settings_data.json`

La paleta VITALYS reemplaza los colores neutros actuales. Los esquemas quedan:
- **scheme-1** (Primary / Cream): fondo Cream, texto Carbon, CTAs Carbon
- **scheme-2** (Secondary / Sand): fondo Sand, texto Carbon, CTAs Carbon  
- **scheme-3** (Accent / Forest): fondo Forest, texto Cream, CTAs Cream
- **scheme-5** (Dark / Carbon): fondo Carbon, texto Cream, CTAs Gold
- **scheme-6** (Transparent / Hero): transparente, texto Cream

- [ ] **Step 1: Actualizar scheme-1 (Cream — pantallas principales)**

En `config/settings_data.json`, dentro de `"current"."color_schemes"."scheme-1"."settings"`, reemplazar todos los valores con:

```json
{
  "background": "#F7F5F0",
  "foreground_heading": "#1C1C1A",
  "foreground": "#1C1C1A",
  "primary": "#1C1C1A",
  "primary_hover": "#1C1C1A",
  "border": "#1C1C1A1A",
  "shadow": "#1C1C1A",
  "primary_button_background": "#1C1C1A",
  "primary_button_text": "#F7F5F0",
  "primary_button_border": "#1C1C1A",
  "primary_button_hover_background": "#3a3a38",
  "primary_button_hover_text": "#F7F5F0",
  "primary_button_hover_border": "#3a3a38",
  "secondary_button_background": "rgba(0,0,0,0)",
  "secondary_button_text": "#1C1C1A",
  "secondary_button_border": "#1C1C1A",
  "secondary_button_hover_background": "#E8E3D9",
  "secondary_button_hover_text": "#1C1C1A",
  "secondary_button_hover_border": "#1C1C1A",
  "input_background": "#F7F5F0",
  "input_text_color": "#1C1C1A",
  "input_border_color": "#1C1C1A40",
  "input_hover_background": "#E8E3D9",
  "variant_background_color": "#F7F5F0",
  "variant_text_color": "#1C1C1A",
  "variant_border_color": "#1C1C1A20",
  "variant_hover_background_color": "#E8E3D9",
  "variant_hover_text_color": "#1C1C1A",
  "variant_hover_border_color": "#1C1C1A40",
  "selected_variant_background_color": "#1C1C1A",
  "selected_variant_text_color": "#F7F5F0",
  "selected_variant_border_color": "#1C1C1A",
  "selected_variant_hover_background_color": "#3a3a38",
  "selected_variant_hover_text_color": "#F7F5F0",
  "selected_variant_hover_border_color": "#3a3a38"
}
```

- [ ] **Step 2: Actualizar scheme-2 (Sand — secciones secundarias)**

En `"scheme-2"."settings"` reemplazar con:

```json
{
  "background": "#E8E3D9",
  "foreground_heading": "#1C1C1A",
  "foreground": "#1C1C1A",
  "primary": "#1C1C1A",
  "primary_hover": "#1C1C1A",
  "border": "#1C1C1A20",
  "shadow": "#1C1C1A",
  "primary_button_background": "#1C1C1A",
  "primary_button_text": "#F7F5F0",
  "primary_button_border": "#1C1C1A",
  "primary_button_hover_background": "#3a3a38",
  "primary_button_hover_text": "#F7F5F0",
  "primary_button_hover_border": "#3a3a38",
  "secondary_button_background": "rgba(0,0,0,0)",
  "secondary_button_text": "#1C1C1A",
  "secondary_button_border": "#1C1C1A",
  "secondary_button_hover_background": "#F7F5F0",
  "secondary_button_hover_text": "#1C1C1A",
  "secondary_button_hover_border": "#1C1C1A",
  "input_background": "rgba(0,0,0,0)",
  "input_text_color": "#1C1C1A",
  "input_border_color": "#1C1C1A30",
  "input_hover_background": "#F7F5F0",
  "variant_background_color": "#F7F5F0",
  "variant_text_color": "#1C1C1A",
  "variant_border_color": "#1C1C1A20",
  "variant_hover_background_color": "#E8E3D9",
  "variant_hover_text_color": "#1C1C1A",
  "variant_hover_border_color": "#1C1C1A40",
  "selected_variant_background_color": "#1C1C1A",
  "selected_variant_text_color": "#F7F5F0",
  "selected_variant_border_color": "#1C1C1A",
  "selected_variant_hover_background_color": "#3a3a38",
  "selected_variant_hover_text_color": "#F7F5F0",
  "selected_variant_hover_border_color": "#3a3a38"
}
```

- [ ] **Step 3: Actualizar scheme-3 (Forest — secciones de acento verde)**

En `"scheme-3"."settings"` reemplazar con:

```json
{
  "background": "#3D5A48",
  "foreground_heading": "#F7F5F0",
  "foreground": "#F7F5F0",
  "primary": "#F7F5F0",
  "primary_hover": "#E8E3D9",
  "border": "#F7F5F030",
  "shadow": "#1C1C1A",
  "primary_button_background": "#F7F5F0",
  "primary_button_text": "#1C1C1A",
  "primary_button_border": "#F7F5F0",
  "primary_button_hover_background": "#E8E3D9",
  "primary_button_hover_text": "#1C1C1A",
  "primary_button_hover_border": "#E8E3D9",
  "secondary_button_background": "rgba(0,0,0,0)",
  "secondary_button_text": "#F7F5F0",
  "secondary_button_border": "#F7F5F060",
  "secondary_button_hover_background": "#F7F5F015",
  "secondary_button_hover_text": "#F7F5F0",
  "secondary_button_hover_border": "#F7F5F080",
  "input_background": "rgba(0,0,0,0)",
  "input_text_color": "#F7F5F0",
  "input_border_color": "#F7F5F050",
  "input_hover_background": "#F7F5F010",
  "variant_background_color": "#F7F5F0",
  "variant_text_color": "#1C1C1A",
  "variant_border_color": "#F7F5F020",
  "variant_hover_background_color": "#E8E3D9",
  "variant_hover_text_color": "#1C1C1A",
  "variant_hover_border_color": "#1C1C1A20",
  "selected_variant_background_color": "#1C1C1A",
  "selected_variant_text_color": "#F7F5F0",
  "selected_variant_border_color": "#1C1C1A",
  "selected_variant_hover_background_color": "#3a3a38",
  "selected_variant_hover_text_color": "#F7F5F0",
  "selected_variant_hover_border_color": "#3a3a38"
}
```

- [ ] **Step 4: Actualizar scheme-5 (Carbon — header y secciones oscuras)**

En `"scheme-5"."settings"` reemplazar con:

```json
{
  "background": "#1C1C1A",
  "foreground_heading": "#F7F5F0",
  "foreground": "#F7F5F0",
  "primary": "#F7F5F0",
  "primary_hover": "#E8E3D9",
  "border": "#F7F5F020",
  "shadow": "#000000",
  "primary_button_background": "#C8A96E",
  "primary_button_text": "#1C1C1A",
  "primary_button_border": "#C8A96E",
  "primary_button_hover_background": "#b8975e",
  "primary_button_hover_text": "#1C1C1A",
  "primary_button_hover_border": "#b8975e",
  "secondary_button_background": "rgba(0,0,0,0)",
  "secondary_button_text": "#F7F5F0",
  "secondary_button_border": "#F7F5F060",
  "secondary_button_hover_background": "#F7F5F010",
  "secondary_button_hover_text": "#F7F5F0",
  "secondary_button_hover_border": "#F7F5F080",
  "input_background": "#1C1C1A",
  "input_text_color": "#F7F5F0",
  "input_border_color": "#F7F5F040",
  "input_hover_background": "#F7F5F00a",
  "variant_background_color": "#F7F5F0",
  "variant_text_color": "#1C1C1A",
  "variant_border_color": "#F7F5F020",
  "variant_hover_background_color": "#E8E3D9",
  "variant_hover_text_color": "#1C1C1A",
  "variant_hover_border_color": "#1C1C1A20",
  "selected_variant_background_color": "#C8A96E",
  "selected_variant_text_color": "#1C1C1A",
  "selected_variant_border_color": "#C8A96E",
  "selected_variant_hover_background_color": "#b8975e",
  "selected_variant_hover_text_color": "#1C1C1A",
  "selected_variant_hover_border_color": "#b8975e"
}
```

- [ ] **Step 5: Actualizar scheme-6 (Transparente / Hero con texto claro)**

En `"scheme-6"."settings"` reemplazar con:

```json
{
  "background": "rgba(0,0,0,0)",
  "foreground_heading": "#F7F5F0",
  "foreground": "#F7F5F0",
  "primary": "#F7F5F0",
  "primary_hover": "#E8E3D9",
  "border": "#F7F5F030",
  "shadow": "#1C1C1A",
  "primary_button_background": "#F7F5F0",
  "primary_button_text": "#1C1C1A",
  "primary_button_border": "#F7F5F0",
  "primary_button_hover_background": "#E8E3D9",
  "primary_button_hover_text": "#1C1C1A",
  "primary_button_hover_border": "#E8E3D9",
  "secondary_button_background": "rgba(0,0,0,0)",
  "secondary_button_text": "#F7F5F0",
  "secondary_button_border": "#F7F5F0",
  "secondary_button_hover_background": "#F7F5F014",
  "secondary_button_hover_text": "#F7F5F0",
  "secondary_button_hover_border": "#F7F5F0",
  "input_background": "#F7F5F0",
  "input_text_color": "#1C1C1A",
  "input_border_color": "#1C1C1A20",
  "input_hover_background": "#E8E3D9",
  "variant_background_color": "#F7F5F0",
  "variant_text_color": "#1C1C1A",
  "variant_border_color": "#1C1C1A20",
  "variant_hover_background_color": "#E8E3D9",
  "variant_hover_text_color": "#1C1C1A",
  "variant_hover_border_color": "#1C1C1A30",
  "selected_variant_background_color": "#1C1C1A",
  "selected_variant_text_color": "#F7F5F0",
  "selected_variant_border_color": "#1C1C1A",
  "selected_variant_hover_background_color": "#3a3a38",
  "selected_variant_hover_text_color": "#F7F5F0",
  "selected_variant_hover_border_color": "#3a3a38"
}
```

- [ ] **Step 6: Verificar JSON válido**

```bash
cd /Users/cris/Desktop/shopify-belevels
python3 -c "import json; json.load(open('config/settings_data.json')); print('JSON válido')"
```

Resultado esperado: `JSON válido`

- [ ] **Step 7: Commit**

```bash
git add config/settings_data.json
git commit -m "feat: apply VITALYS color palette to all Shopify color schemes"
```

---

## Task 2: Tipografía VITALYS en settings_data.json

**Files:**
- Modify: `config/settings_data.json`

Reemplaza Inter por Playfair Display (headings) + DM Sans (body). Ajusta tamaños para mayor presencia visual y border-radius más sobrio.

- [ ] **Step 1: Actualizar fuentes y tamaños tipográficos**

En `config/settings_data.json`, dentro de `"current"`, actualizar estos campos (manteniendo el resto intacto):

```json
"type_body_font": "dm_sans_n4",
"type_subheading_font": "dm_sans_n5",
"type_heading_font": "playfair_display_n4",
"type_accent_font": "dm_sans_n5",
"type_size_paragraph": "14",
"type_line_height_paragraph": "body-loose",
"type_font_h1": "heading",
"type_size_h1": "88",
"type_line_height_h1": "display-tight",
"type_letter_spacing_h1": "heading-tight",
"type_case_h1": "none",
"type_font_h2": "heading",
"type_size_h2": "56",
"type_line_height_h2": "display-tight",
"type_letter_spacing_h2": "heading-tight",
"type_case_h2": "none",
"type_font_h3": "heading",
"type_size_h3": "40",
"type_line_height_h3": "display-normal",
"type_letter_spacing_h3": "heading-normal",
"type_case_h3": "none",
"type_font_h4": "subheading",
"type_size_h4": "20",
"type_line_height_h4": "display-tight",
"type_font_h5": "subheading",
"type_size_h5": "14",
"type_line_height_h5": "display-loose",
"type_font_h6": "subheading",
"type_size_h6": "11",
"type_line_height_h6": "display-loose",
"button_border_radius_primary": 4,
"button_border_radius_secondary": 4,
"inputs_border_radius": 4,
"card_corner_radius": 4,
"badge_corner_radius": 4
```

- [ ] **Step 2: Verificar JSON válido**

```bash
python3 -c "import json; json.load(open('config/settings_data.json')); print('JSON válido')"
```

Resultado esperado: `JSON válido`

- [ ] **Step 3: Commit**

```bash
git add config/settings_data.json
git commit -m "feat: apply VITALYS typography — Playfair Display headings, DM Sans body"
```

---

## Task 3: CSS custom properties de marca VITALYS

**Files:**
- Create: `assets/vitalys.css`
- Modify: `layout/theme.liquid`

Añade los tokens Gold/Forest/Cream/Carbon/Sand como variables CSS globales, más overrides de estilo propios de VITALYS que no se pueden hacer desde los esquemas de color.

- [ ] **Step 1: Crear assets/vitalys.css**

```css
/* VITALYS Brand Tokens */
:root {
  --vitalys-cream: #F7F5F0;
  --vitalys-carbon: #1C1C1A;
  --vitalys-gold: #C8A96E;
  --vitalys-gold-hover: #b8975e;
  --vitalys-sand: #E8E3D9;
  --vitalys-forest: #3D5A48;
}

/* Gold accent — badges, labels, category pills */
.vitalys-badge-gold {
  background: var(--vitalys-gold);
  color: var(--vitalys-carbon);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  padding: 3px 10px;
  border-radius: 20px;
  display: inline-block;
}

/* Forest badge — naturaleza, ingredientes */
.vitalys-badge-forest {
  background: var(--vitalys-forest);
  color: var(--vitalys-cream);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  padding: 3px 10px;
  border-radius: 20px;
  display: inline-block;
}

/* Trust bar icon row */
.vitalys-trust-row {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
  align-items: center;
  padding: 12px 0;
}

.vitalys-trust-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.5px;
  color: var(--color-foreground);
}

/* Ingredient highlight block */
.vitalys-ingredient-highlight {
  border-left: 3px solid var(--vitalys-gold);
  padding: 16px 20px;
  background: var(--vitalys-sand);
  border-radius: 0 6px 6px 0;
  margin: 16px 0;
}

.vitalys-ingredient-highlight .ingredient-name {
  font-size: 16px;
  font-weight: 500;
  color: var(--vitalys-carbon);
  margin-bottom: 4px;
}

.vitalys-ingredient-highlight .ingredient-dose {
  font-size: 13px;
  color: var(--vitalys-forest);
  font-weight: 500;
  margin-bottom: 6px;
}

.vitalys-ingredient-highlight .ingredient-why {
  font-size: 13px;
  color: var(--vitalys-carbon);
  opacity: 0.75;
  line-height: 1.5;
}

/* Heading override: h1, h2 use Playfair Display with negative letter-spacing */
h1, h2 {
  letter-spacing: -0.03em;
}

/* Marquee trust bar text styling */
.marquee-text {
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 2px;
  text-transform: uppercase;
}
```

- [ ] **Step 2: Enlazar vitalys.css en layout/theme.liquid**

Leer `layout/theme.liquid` y localizar la línea que contiene `</head>`. Añadir la línea siguiente justo antes de `</head>`:

```liquid
<link rel="stylesheet" href="{{ 'vitalys.css' | asset_url }}" media="all">
```

- [ ] **Step 3: Verificar que el archivo existe**

```bash
ls -la /Users/cris/Desktop/shopify-belevels/assets/vitalys.css
```

Resultado esperado: muestra el archivo con tamaño > 0.

- [ ] **Step 4: Commit**

```bash
git add assets/vitalys.css layout/theme.liquid
git commit -m "feat: add VITALYS brand CSS custom properties and utility classes"
```

---

## Task 4: Homepage VITALYS — templates/index.json

**Files:**
- Modify: `templates/index.json`

Reemplaza la homepage actual (hero genérico + product-list) con la estructura VITALYS de 8 secciones. Las secciones usan tipos que ya existen en el tema (`hero`, `marquee`, `collection-links`, `product-list`, `media-with-content`).

- [ ] **Step 1: Reemplazar templates/index.json**

Sobreescribir el archivo completo con:

```json
{
  "sections": {
    "hero_vitalys": {
      "type": "hero",
      "blocks": {
        "eyebrow": {
          "type": "text",
          "name": "Eyebrow",
          "settings": {
            "text": "<p>Formulación europea · Dosificación clínica</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "h6",
            "font": "var(--font-body--family)",
            "font_size": "0.75rem",
            "line_height": "normal",
            "letter_spacing": "loose",
            "case": "uppercase",
            "wrap": "pretty",
            "color": "var(--vitalys-gold, #C8A96E)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 8,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "headline": {
          "type": "text",
          "name": "Headline",
          "settings": {
            "text": "<h1>La diferencia está en lo que no se ve.</h1>",
            "width": "fit-content",
            "max_width": "narrow",
            "alignment": "left",
            "type_preset": "h1",
            "font": "var(--font-heading--family)",
            "font_size": "",
            "line_height": "normal",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground-heading)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 16,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "subheadline": {
          "type": "text",
          "name": "Subheadline",
          "settings": {
            "text": "<p>Suplementos con ingredientes europeos certificados y dosificación clínica. Sin rellenos, sin atajos.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "1rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 24,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "cta": {
          "type": "button",
          "name": "CTA",
          "settings": {
            "label": "Descubrir productos →",
            "link": "shopify://collections/all",
            "open_in_new_tab": false,
            "style_class": "button",
            "width": "fit-content",
            "custom_width": 100,
            "width_mobile": "fit-content",
            "custom_width_mobile": 100
          },
          "blocks": {}
        }
      },
      "block_order": ["eyebrow", "headline", "subheadline", "cta"],
      "name": "Hero VITALYS",
      "settings": {
        "media_type_1": "image",
        "media_type_2": "image",
        "stack_media_on_mobile": false,
        "custom_mobile_media": false,
        "media_type_1_mobile": "image",
        "media_type_2_mobile": "image",
        "open_in_new_tab": false,
        "content_direction": "column",
        "vertical_on_mobile": true,
        "horizontal_alignment": "flex-start",
        "vertical_alignment": "flex-end",
        "align_baseline": false,
        "horizontal_alignment_flex_direction_column": "flex-start",
        "vertical_alignment_flex_direction_column": "flex-end",
        "gap": 0,
        "section_width": "page-width",
        "section_height": "large",
        "section_height_custom": 80,
        "color_scheme": "scheme-6",
        "toggle_overlay": true,
        "overlay_color": "#1C1C1A55",
        "overlay_style": "gradient",
        "gradient_direction": "to top",
        "blurred_reflection": false,
        "reflection_opacity": 75,
        "padding-block-start": 80,
        "padding-block-end": 64
      }
    },
    "trust_marquee": {
      "type": "marquee",
      "blocks": {
        "item1": {
          "type": "_marquee",
          "settings": {
            "text": "Fabricado en Europa",
            "icon": "leaf"
          },
          "blocks": {}
        },
        "item2": {
          "type": "_marquee",
          "settings": {
            "text": "Fórmula clínica",
            "icon": "flask"
          },
          "blocks": {}
        },
        "item3": {
          "type": "_marquee",
          "settings": {
            "text": "Sin dióxido de titanio",
            "icon": "checkmark"
          },
          "blocks": {}
        },
        "item4": {
          "type": "_marquee",
          "settings": {
            "text": "Nutricionistas propios",
            "icon": "person"
          },
          "blocks": {}
        },
        "item5": {
          "type": "_marquee",
          "settings": {
            "text": "+4.800 valoraciones",
            "icon": "star"
          },
          "blocks": {}
        }
      },
      "block_order": ["item1", "item2", "item3", "item4", "item5"],
      "name": "Trust Bar",
      "settings": {
        "speed": 40,
        "pause_on_hover": false,
        "color_scheme": "scheme-2",
        "padding-block-start": 12,
        "padding-block-end": 12
      }
    },
    "objetivos_grid": {
      "type": "collection-links",
      "blocks": {},
      "block_order": [],
      "name": "¿Cuál es tu objetivo?",
      "settings": {
        "heading": "¿Cuál es tu objetivo?",
        "menu": "main-menu",
        "image_ratio": "square",
        "columns": 5,
        "mobile_columns": "2",
        "section_width": "page-width",
        "color_scheme": "scheme-1",
        "padding-block-start": 64,
        "padding-block-end": 48
      }
    },
    "bestsellers": {
      "type": "product-list",
      "blocks": {
        "static-header": {
          "type": "_product-list-content",
          "name": "Header",
          "static": true,
          "settings": {
            "content_direction": "row",
            "vertical_on_mobile": false,
            "horizontal_alignment": "space-between",
            "vertical_alignment": "flex-end",
            "align_baseline": true,
            "horizontal_alignment_flex_direction_column": "flex-start",
            "vertical_alignment_flex_direction_column": "center",
            "gap": 12,
            "width": "fill",
            "custom_width": 100,
            "width_mobile": "fill",
            "custom_width_mobile": 100,
            "height": "fit",
            "custom_height": 100,
            "inherit_color_scheme": true,
            "color_scheme": "",
            "background_media": "none",
            "video_position": "cover",
            "background_image_position": "cover",
            "border": "none",
            "border_width": 1,
            "border_opacity": 100,
            "border_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {
            "heading": {
              "type": "_product-list-text",
              "name": "Heading",
              "settings": {
                "text": "<h2>Los más valorados</h2>",
                "width": "fit-content",
                "max_width": "normal",
                "alignment": "left",
                "type_preset": "h3",
                "font": "var(--font-heading--family)",
                "font_size": "",
                "line_height": "normal",
                "letter_spacing": "normal",
                "case": "none",
                "wrap": "pretty",
                "color": "var(--color-foreground)",
                "background": false,
                "background_color": "#00000026",
                "corner_radius": 0,
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "view_all": {
              "type": "_product-list-button",
              "name": "Ver todos",
              "settings": {
                "label": "Ver todos →",
                "open_in_new_tab": false,
                "style_class": "link",
                "width": "fit-content",
                "custom_width": 100,
                "width_mobile": "fit-content",
                "custom_width_mobile": 100
              },
              "blocks": {}
            }
          },
          "block_order": ["heading", "view_all"]
        },
        "static-product-card": {
          "type": "_product-card",
          "name": "Product card",
          "static": true,
          "settings": {
            "product_card_gap": 4,
            "inherit_color_scheme": true,
            "color_scheme": "",
            "border": "none",
            "border_width": 1,
            "border_opacity": 100,
            "border_radius": 4,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {
            "gallery": {
              "type": "_product-card-gallery",
              "name": "Gallery",
              "settings": {
                "image_ratio": "square",
                "border": "none",
                "border_width": 1,
                "border_opacity": 100,
                "border_radius": 4,
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "title": {
              "type": "product-title",
              "name": "Título",
              "settings": {
                "width": "100%",
                "max_width": "normal",
                "alignment": "left",
                "type_preset": "rte",
                "font": "var(--font-body--family)",
                "font_size": "0.875rem",
                "line_height": "normal",
                "letter_spacing": "normal",
                "case": "none",
                "wrap": "pretty",
                "color": "var(--color-foreground)",
                "background": false,
                "background_color": "#00000026",
                "corner_radius": 0,
                "padding-block-start": 8,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "price": {
              "type": "price",
              "settings": {
                "show_sale_price_first": true,
                "show_installments": false,
                "show_tax_info": false,
                "type_preset": "paragraph",
                "width": "100%",
                "alignment": "left",
                "font": "var(--font-body--family)",
                "font_size": "0.875rem",
                "line_height": "normal",
                "letter_spacing": "normal",
                "case": "none",
                "color": "var(--color-foreground)",
                "padding-block-start": 2,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            }
          },
          "block_order": ["gallery", "title", "price"]
        }
      },
      "name": "Bestsellers",
      "settings": {
        "collection": "all",
        "layout_type": "grid",
        "carousel_on_mobile": true,
        "max_products": 4,
        "columns": 4,
        "mobile_columns": "1",
        "mobile_card_size": "75cqw",
        "columns_gap": 12,
        "rows_gap": 24,
        "icons_style": "arrow",
        "icons_shape": "circle",
        "section_width": "page-width",
        "horizontal_alignment": "flex-start",
        "gap": 32,
        "color_scheme": "scheme-1",
        "padding-block-start": 64,
        "padding-block-end": 64
      }
    },
    "pilares_vitalys": {
      "type": "media-with-content",
      "blocks": {
        "eyebrow": {
          "type": "text",
          "name": "Eyebrow",
          "settings": {
            "text": "<p>Por qué VITALYS</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "h6",
            "font": "var(--font-body--family)",
            "font_size": "0.75rem",
            "line_height": "normal",
            "letter_spacing": "loose",
            "case": "uppercase",
            "wrap": "pretty",
            "color": "var(--vitalys-gold, #C8A96E)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 8,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "heading": {
          "type": "text",
          "name": "Heading",
          "settings": {
            "text": "<h2>La formulación que no cede.</h2>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "h2",
            "font": "var(--font-heading--family)",
            "font_size": "",
            "line_height": "normal",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground-heading)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 20,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "pilar1": {
          "type": "text",
          "name": "Pilar 1",
          "settings": {
            "text": "<p><strong>Ingredientes europeos certificados</strong><br>Trazabilidad completa, sin materias primas de origen opaco.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "0.9375rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 12,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "pilar2": {
          "type": "text",
          "name": "Pilar 2",
          "settings": {
            "text": "<p><strong>Dosificación clínica exacta</strong><br>Las cantidades que usan los estudios, no las que abaratan el producto.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "0.9375rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 12,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "pilar3": {
          "type": "text",
          "name": "Pilar 3",
          "settings": {
            "text": "<p><strong>Fórmulas propias, sin copiar</strong><br>Cada producto diseñado desde cero por nuestro equipo de nutricionistas.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "0.9375rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 12,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "pilar4": {
          "type": "text",
          "name": "Pilar 4",
          "settings": {
            "text": "<p><strong>Sin rellenos innecesarios</strong><br>Lo que no está en el envase importa tanto como lo que sí está.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "0.9375rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        }
      },
      "block_order": ["eyebrow", "heading", "pilar1", "pilar2", "pilar3", "pilar4"],
      "name": "Los 4 Pilares",
      "settings": {
        "media_type": "image",
        "desktop_media_position": "right",
        "content_direction": "column",
        "horizontal_alignment": "flex-start",
        "vertical_alignment": "center",
        "gap": 24,
        "section_width": "page-width",
        "color_scheme": "scheme-2",
        "padding-block-start": 80,
        "padding-block-end": 80
      }
    },
    "ingrediente_destacado": {
      "type": "media-with-content",
      "blocks": {
        "eyebrow": {
          "type": "text",
          "name": "Eyebrow",
          "settings": {
            "text": "<p>Transparencia de fórmula</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "h6",
            "font": "var(--font-body--family)",
            "font_size": "0.75rem",
            "line_height": "normal",
            "letter_spacing": "loose",
            "case": "uppercase",
            "wrap": "pretty",
            "color": "var(--vitalys-gold, #C8A96E)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 8,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "heading": {
          "type": "text",
          "name": "Heading",
          "settings": {
            "text": "<h2>Cada miligramo tiene un motivo.</h2>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "h2",
            "font": "var(--font-heading--family)",
            "font_size": "",
            "line_height": "normal",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground-heading)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 20,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "ingrediente_content": {
          "type": "text",
          "name": "Ingrediente",
          "settings": {
            "text": "<p><strong>Magnesio bisglicinato · 300 mg por dosis</strong><br>La forma de magnesio con mayor biodisponibilidad — absorbida 4× mejor que el óxido de magnesio. Elegida no por ser la más barata, sino porque funciona.</p><p><strong>Sin rellenos. Sin excepciones.</strong> Publicamos las dosis exactas de todos nuestros ingredientes. Ninguna fórmula propietaria que oculte cantidades.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "0.9375rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 24,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "cta": {
          "type": "button",
          "name": "CTA",
          "settings": {
            "label": "Ver todos los productos →",
            "link": "shopify://collections/all",
            "open_in_new_tab": false,
            "style_class": "button-secondary",
            "width": "fit-content",
            "custom_width": 100,
            "width_mobile": "fit-content",
            "custom_width_mobile": 100
          },
          "blocks": {}
        }
      },
      "block_order": ["eyebrow", "heading", "ingrediente_content", "cta"],
      "name": "Transparencia de Fórmula",
      "settings": {
        "media_type": "image",
        "desktop_media_position": "left",
        "content_direction": "column",
        "horizontal_alignment": "flex-start",
        "vertical_alignment": "center",
        "gap": 24,
        "section_width": "page-width",
        "color_scheme": "scheme-1",
        "padding-block-start": 80,
        "padding-block-end": 80
      }
    },
    "quiz_cta": {
      "type": "media-with-content",
      "blocks": {
        "heading": {
          "type": "text",
          "name": "Heading",
          "settings": {
            "text": "<h2>¿No sabes por dónde empezar?</h2>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "center",
            "type_preset": "h2",
            "font": "var(--font-heading--family)",
            "font_size": "",
            "line_height": "normal",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground-heading)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 16,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "subtext": {
          "type": "text",
          "name": "Subtext",
          "settings": {
            "text": "<p>3 preguntas. 1 recomendación personalizada. Sin compromiso.</p>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "center",
            "type_preset": "paragraph",
            "font": "var(--font-body--family)",
            "font_size": "1rem",
            "line_height": "loose",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 24,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "cta": {
          "type": "button",
          "name": "CTA quiz",
          "settings": {
            "label": "Hacer el diagnóstico →",
            "link": "/pages/quiz",
            "open_in_new_tab": false,
            "style_class": "button",
            "width": "fit-content",
            "custom_width": 100,
            "width_mobile": "fill",
            "custom_width_mobile": 100
          },
          "blocks": {}
        }
      },
      "block_order": ["heading", "subtext", "cta"],
      "name": "Quiz Diagnóstico",
      "settings": {
        "media_type": "none",
        "desktop_media_position": "right",
        "content_direction": "column",
        "horizontal_alignment": "center",
        "vertical_alignment": "center",
        "gap": 0,
        "section_width": "page-width",
        "color_scheme": "scheme-2",
        "padding-block-start": 80,
        "padding-block-end": 80
      }
    }
  },
  "order": [
    "hero_vitalys",
    "trust_marquee",
    "objetivos_grid",
    "bestsellers",
    "pilares_vitalys",
    "ingrediente_destacado",
    "quiz_cta"
  ]
}
```

- [ ] **Step 2: Verificar JSON válido**

```bash
python3 -c "import json; json.load(open('templates/index.json')); print('JSON válido')"
```

Resultado esperado: `JSON válido`

- [ ] **Step 3: Commit**

```bash
git add templates/index.json
git commit -m "feat: rebuild VITALYS homepage with 7-section structure"
```

---

## Task 5: Página de Producto VITALYS — templates/product.json

**Files:**
- Modify: `templates/product.json`

Añade bloques de beneficio principal, trust icons, FAQ (accordion), y mejora el texto de la sección de recomendaciones. La galería y el núcleo de compra (variantes + botón) se mantienen del template original.

- [ ] **Step 1: Reemplazar templates/product.json**

Sobreescribir el archivo completo con:

```json
{
  "sections": {
    "main": {
      "type": "product-information",
      "blocks": {
        "media-gallery": {
          "type": "_product-media-gallery",
          "static": true,
          "settings": {
            "media_presentation": "grid",
            "media_columns": "two",
            "image_gap": 4,
            "large_first_image": true,
            "icons_style": "none",
            "slideshow_controls_style": "counter",
            "slideshow_mobile_controls_style": "dots",
            "thumbnail_position": "left",
            "thumbnail_width": 56,
            "aspect_ratio": "square",
            "constrain_to_viewport": true,
            "media_fit": "contain",
            "media_radius": 4,
            "extend_media": false,
            "zoom": true,
            "video_loop": false,
            "hide_variants": true,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "product-details": {
          "type": "_product-details",
          "static": true,
          "settings": {
            "width": "fill",
            "custom_width": 100,
            "width_mobile": "fill",
            "custom_width_mobile": 100,
            "height": "fit",
            "details_position": "flex-start",
            "gap": 20,
            "sticky_details_desktop": true,
            "inherit_color_scheme": true,
            "color_scheme": "scheme-1",
            "background_media": "none",
            "video_position": "cover",
            "background_image_position": "cover",
            "border": "none",
            "border_width": 1,
            "border_opacity": 100,
            "border_radius": 0,
            "padding-block-start": 24,
            "padding-block-end": 24,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {
            "header_group": {
              "type": "group",
              "name": "Nombre y precio",
              "settings": {
                "open_in_new_tab": false,
                "content_direction": "column",
                "vertical_on_mobile": true,
                "horizontal_alignment": "flex-start",
                "vertical_alignment": "center",
                "align_baseline": false,
                "horizontal_alignment_flex_direction_column": "flex-start",
                "vertical_alignment_flex_direction_column": "center",
                "gap": 8,
                "width": "fill",
                "custom_width": 100,
                "width_mobile": "fill",
                "custom_width_mobile": 100,
                "height": "fit",
                "custom_height": 100,
                "inherit_color_scheme": true,
                "color_scheme": "",
                "background_media": "none",
                "video_position": "cover",
                "background_image_position": "cover",
                "border": "none",
                "border_width": 1,
                "border_opacity": 100,
                "border_radius": 0,
                "toggle_overlay": false,
                "overlay_color": "#00000026",
                "overlay_style": "solid",
                "gradient_direction": "to top",
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {
                "title": {
                  "type": "text",
                  "name": "Título",
                  "settings": {
                    "text": "<h1>{{ closest.product.title }}</h1>",
                    "width": "100%",
                    "max_width": "normal",
                    "alignment": "left",
                    "type_preset": "h3",
                    "font": "var(--font-heading--family)",
                    "font_size": "",
                    "line_height": "normal",
                    "letter_spacing": "normal",
                    "case": "none",
                    "wrap": "pretty",
                    "color": "var(--color-foreground-heading)",
                    "background": false,
                    "background_color": "#00000026",
                    "corner_radius": 0,
                    "padding-block-start": 0,
                    "padding-block-end": 0,
                    "padding-inline-start": 0,
                    "padding-inline-end": 0
                  },
                  "blocks": {}
                },
                "price": {
                  "type": "price",
                  "settings": {
                    "show_sale_price_first": true,
                    "show_installments": false,
                    "show_tax_info": false,
                    "type_preset": "paragraph",
                    "width": "100%",
                    "alignment": "left",
                    "font": "var(--font-body--family)",
                    "font_size": "1.125rem",
                    "line_height": "normal",
                    "letter_spacing": "normal",
                    "case": "none",
                    "color": "var(--color-foreground)",
                    "padding-block-start": 0,
                    "padding-block-end": 0,
                    "padding-inline-start": 0,
                    "padding-inline-end": 0
                  },
                  "blocks": {}
                }
              },
              "block_order": ["title", "price"]
            },
            "divider_top": {
              "type": "_divider",
              "name": "Separador",
              "settings": {
                "thickness": 1,
                "corner_radius": "square",
                "width_percent": 100,
                "padding-block-start": 4,
                "padding-block-end": 4
              },
              "blocks": {}
            },
            "variant_picker": {
              "type": "variant-picker",
              "settings": {
                "variant_style": "buttons",
                "show_swatches": false,
                "alignment": "left",
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "buy_buttons": {
              "type": "buy-buttons",
              "settings": {
                "stacking": true,
                "show_pickup_availability": false,
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {
                "quantity": {
                  "type": "quantity",
                  "static": true,
                  "settings": {},
                  "blocks": {}
                },
                "add-to-cart": {
                  "type": "add-to-cart",
                  "static": true,
                  "settings": {
                    "style_class": "button"
                  },
                  "blocks": {}
                },
                "accelerated-checkout": {
                  "type": "accelerated-checkout",
                  "static": true,
                  "settings": {},
                  "blocks": {}
                }
              },
              "block_order": []
            },
            "trust_icons": {
              "type": "text",
              "name": "Trust icons",
              "settings": {
                "text": "<p>✓ Fabricado en UE &nbsp;&nbsp; ✓ Sin dióxido de titanio &nbsp;&nbsp; ✓ GMP certificado &nbsp;&nbsp; ✓ Envío en 24h</p>",
                "width": "100%",
                "max_width": "normal",
                "alignment": "left",
                "type_preset": "paragraph",
                "font": "var(--font-body--family)",
                "font_size": "0.75rem",
                "line_height": "normal",
                "letter_spacing": "normal",
                "case": "none",
                "wrap": "pretty",
                "color": "var(--color-foreground)",
                "background": true,
                "background_color": "#E8E3D9",
                "corner_radius": 4,
                "padding-block-start": 10,
                "padding-block-end": 10,
                "padding-inline-start": 14,
                "padding-inline-end": 14
              },
              "blocks": {}
            },
            "divider_mid": {
              "type": "_divider",
              "name": "Separador",
              "settings": {
                "thickness": 1,
                "corner_radius": "square",
                "width_percent": 100,
                "padding-block-start": 4,
                "padding-block-end": 4
              },
              "blocks": {}
            },
            "description": {
              "type": "text",
              "name": "Descripción",
              "settings": {
                "text": "{{ closest.product.description }}",
                "width": "100%",
                "max_width": "normal",
                "alignment": "left",
                "type_preset": "rte",
                "font": "var(--font-body--family)",
                "font_size": "",
                "line_height": "loose",
                "letter_spacing": "normal",
                "case": "none",
                "wrap": "pretty",
                "color": "var(--color-foreground)",
                "background": false,
                "background_color": "#00000026",
                "corner_radius": 0,
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "faq_accordion": {
              "type": "accordion",
              "name": "Preguntas frecuentes",
              "settings": {
                "heading": "Preguntas frecuentes",
                "heading_preset": "h5",
                "icon": "chevron",
                "open_first_row": false,
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {
                "faq1": {
                  "type": "_accordion-row",
                  "settings": {
                    "heading": "¿Es apto para veganos?",
                    "content": "<p>Sí. Todos los ingredientes de este producto son de origen vegetal o síntesis química, sin derivados animales.</p>"
                  },
                  "blocks": {}
                },
                "faq2": {
                  "type": "_accordion-row",
                  "settings": {
                    "heading": "¿Cuándo empiezo a notar efecto?",
                    "content": "<p>Depende del ingrediente y tu punto de partida. Los resultados sostenibles requieren entre 2 y 6 semanas de uso continuado. No vendemos efectos inmediatos porque no existen.</p>"
                  },
                  "blocks": {}
                },
                "faq3": {
                  "type": "_accordion-row",
                  "settings": {
                    "heading": "¿Puedo tomarlo con otros suplementos?",
                    "content": "<p>En general, sí. Consulta las notas de compatibilidad en la descripción del producto. Si tienes dudas, nuestros nutricionistas están disponibles para asesorarte sin coste.</p>"
                  },
                  "blocks": {}
                },
                "faq4": {
                  "type": "_accordion-row",
                  "settings": {
                    "heading": "¿Tiene alérgenos?",
                    "content": "<p>La información de alérgenos está detallada en la tabla de ingredientes. Fabricamos en instalaciones que pueden contener trazas de gluten, soja y lácteos.</p>"
                  },
                  "blocks": {}
                },
                "faq5": {
                  "type": "_accordion-row",
                  "settings": {
                    "heading": "¿Qué pasa si me salto un día?",
                    "content": "<p>Nada. La consistencia importa a largo plazo, no la perfección diaria. Sigue con tu pauta habitual al día siguiente.</p>"
                  },
                  "blocks": {}
                }
              },
              "block_order": ["faq1", "faq2", "faq3", "faq4", "faq5"]
            }
          },
          "block_order": [
            "header_group",
            "divider_top",
            "variant_picker",
            "buy_buttons",
            "trust_icons",
            "divider_mid",
            "description",
            "faq_accordion"
          ]
        }
      },
      "settings": {
        "content_width": "content-center-aligned",
        "desktop_media_position": "left",
        "equal_columns": false,
        "limit_details_width": true,
        "gap": 48,
        "color_scheme": "scheme-1",
        "padding-block-start": 0,
        "padding-block-end": 0
      }
    },
    "complementarios": {
      "type": "product-recommendations",
      "blocks": {
        "heading": {
          "type": "text",
          "name": "Heading",
          "settings": {
            "text": "<h3>Combina bien con...</h3>",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "type_preset": "h4",
            "font": "var(--font-heading--family)",
            "font_size": "",
            "line_height": "normal",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "pretty",
            "color": "var(--color-foreground-heading)",
            "background": false,
            "background_color": "#00000026",
            "corner_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {}
        },
        "static-product-card": {
          "type": "_product-card",
          "name": "Product card",
          "static": true,
          "settings": {
            "product_card_gap": 8,
            "inherit_color_scheme": true,
            "color_scheme": "",
            "border": "none",
            "border_width": 1,
            "border_opacity": 100,
            "border_radius": 4,
            "padding-block-start": 0,
            "padding-block-end": 8,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {
            "gallery": {
              "type": "_product-card-gallery",
              "name": "Gallery",
              "settings": {
                "image_ratio": "square",
                "border": "none",
                "border_width": 1,
                "border_opacity": 100,
                "border_radius": 4,
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "title": {
              "type": "product-title",
              "name": "Título",
              "settings": {
                "width": "100%",
                "max_width": "normal",
                "alignment": "left",
                "type_preset": "rte",
                "font": "var(--font-body--family)",
                "font_size": "0.875rem",
                "line_height": "normal",
                "letter_spacing": "normal",
                "case": "none",
                "wrap": "pretty",
                "color": "var(--color-foreground)",
                "background": false,
                "background_color": "#00000026",
                "corner_radius": 0,
                "padding-block-start": 4,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            },
            "price": {
              "type": "price",
              "settings": {
                "show_sale_price_first": true,
                "show_installments": false,
                "show_tax_info": false,
                "type_preset": "paragraph",
                "width": "100%",
                "alignment": "left",
                "font": "var(--font-body--family)",
                "font_size": "0.875rem",
                "line_height": "normal",
                "letter_spacing": "normal",
                "case": "none",
                "color": "var(--color-foreground)",
                "padding-block-start": 0,
                "padding-block-end": 0,
                "padding-inline-start": 0,
                "padding-inline-end": 0
              },
              "blocks": {}
            }
          },
          "block_order": ["gallery", "title", "price"]
        }
      },
      "block_order": ["heading"],
      "name": "Combina bien con...",
      "settings": {
        "product": "{{ closest.product }}",
        "recommendation_type": "related",
        "layout_type": "grid",
        "carousel_on_mobile": true,
        "max_products": 3,
        "columns": 3,
        "mobile_columns": "1",
        "mobile_card_size": "75cqw",
        "columns_gap": 12,
        "rows_gap": 24,
        "icons_style": "arrow",
        "icons_shape": "circle",
        "section_width": "page-width",
        "gap": 32,
        "color_scheme": "scheme-2",
        "padding-block-start": 64,
        "padding-block-end": 64
      }
    }
  },
  "order": [
    "main",
    "complementarios"
  ]
}
```

- [ ] **Step 2: Verificar JSON válido**

```bash
python3 -c "import json; json.load(open('templates/product.json')); print('JSON válido')"
```

Resultado esperado: `JSON válido`

- [ ] **Step 3: Commit**

```bash
git add templates/product.json
git commit -m "feat: rebuild VITALYS product page with trust icons, FAQ accordion and complementary products"
```

---

## Verificación final

Después de completar los 5 tasks, verifica el resultado completo:

```bash
# Verificar todos los JSON del proyecto
python3 -c "
import json, os
files = ['config/settings_data.json', 'templates/index.json', 'templates/product.json']
for f in files:
    try:
        json.load(open(f))
        print(f'✓ {f}')
    except Exception as e:
        print(f'✗ {f}: {e}')
"
```

Resultado esperado:
```
✓ config/settings_data.json
✓ templates/index.json
✓ templates/product.json
```

Para previsualizar en Shopify (requiere Shopify CLI instalado):

```bash
shopify theme dev
```

Abre el preview en el navegador y verifica:
- Homepage: paleta Cream/Carbon, Playfair Display en headlines, 7 secciones en orden correcto
- Producto: FAQ accordion visible, trust icons en banda Sand, sección "Combina bien con" con fondo Sand

---

*Plan generado: 2026-05-24 · Basado en VITALYS-brand.md aprobado · Tema: Shopify Horizon*
