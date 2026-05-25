# VITALYS Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the VITALYS homepage — 7 sections in Shopify Liquid using the Horizon theme, following the brand PRD at `docs/VITALYS-PRD.md`.

**Architecture:** Two new custom Liquid sections (`vitalys-benefits.liquid`, `vitalys-testimonial.liquid`) handle the visuals that Horizon's generic sections cannot (icon grid, testimonial card). Everything else uses existing Horizon sections configured via `templates/index.json`. CSS for the new components is added to `assets/vitalys.css`. The footer is updated in `sections/footer-group.json`.

**Tech Stack:** Shopify Liquid, Horizon theme sections, Shopify JSON templates, `assets/vitalys.css` (existing brand token file)

---

## File Map

| Action | File | Responsibility |
|--------|------|---------------|
| Create | `sections/vitalys-benefits.liquid` | 3-column benefit grid with inline SVG icons and schema |
| Create | `sections/vitalys-testimonial.liquid` | Single featured review — photo, stars, blockquote, author |
| Modify | `assets/vitalys.css` | Append CSS for `.vitalys-benefits__*` and `.vitalys-testimonial__*` |
| Replace | `templates/index.json` | New 7-section homepage order with all settings and copy |
| Modify | `sections/footer-group.json` | VITALYS copy + scheme-5 (Carbon) color |

---

## Task 1: Create `sections/vitalys-benefits.liquid`

**Files:**
- Create: `sections/vitalys-benefits.liquid`

- [ ] **Step 1: Create the section file**

Create `/Users/cris/Desktop/shopify-belevels/sections/vitalys-benefits.liquid` with this exact content:

```liquid
{%- if section.settings.heading != blank -%}
  <div class="section-background color-{{ section.settings.color_scheme }}"></div>
{%- endif -%}
<section
  class="section section--{{ section.settings.section_width }} vitalys-benefits color-{{ section.settings.color_scheme }}"
  style="{%- render 'spacing-style', settings: section.settings %}"
  data-section-id="{{ section.id }}"
>
  {%- if section.settings.heading != blank -%}
    <div class="vitalys-benefits__header">
      <h2 class="vitalys-benefits__heading">{{ section.settings.heading }}</h2>
      {%- if section.settings.subheading != blank -%}
        <p class="vitalys-benefits__subheading">{{ section.settings.subheading }}</p>
      {%- endif -%}
    </div>
  {%- endif -%}

  <div class="vitalys-benefits__grid">
    {%- for block in section.blocks -%}
      <div class="vitalys-benefits__item" {{ block.shopify_attributes }}>
        <div class="vitalys-benefits__icon" aria-hidden="true">
          {%- case block.settings.icon -%}
            {%- when 'leaf' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M11 20A7 7 0 0 1 9.8 6.1C15.5 5 17 4.48 19 2c1 2 2 4.18 2 8 0 5.5-4.78 10-10 10z"/><path d="M2 21c0-3 1.85-5.36 5.08-6C9.5 14.52 12 13 13 12"/></svg>
            {%- when 'microscope' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M6 18h8"/><path d="M3 22h18"/><path d="M14 22a7 7 0 1 0 0-14h-1"/><path d="M9 14h2"/><path d="M9 12a2 2 0 0 1-2-2V6h6v4a2 2 0 0 1-2 2Z"/><path d="M12 6V3a1 1 0 0 0-1-1H9a1 1 0 0 0-1 1v3"/></svg>
            {%- when 'shield' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M20 13c0 5-3.5 7.5-7.66 8.95a1 1 0 0 1-.67-.01C7.5 20.5 4 18 4 13V6a1 1 0 0 1 1-1c2 0 4.5-1.2 6.24-2.72a1.17 1.17 0 0 1 1.52 0C14.51 3.81 17 5 19 5a1 1 0 0 1 1 1z"/></svg>
            {%- when 'check' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><path d="m9 11 3 3L22 4"/></svg>
            {%- when 'flask' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.5 2v17.5c0 1.4-1.1 2.5-2.5 2.5h0c-1.4 0-2.5-1.1-2.5-2.5V2"/><path d="M8.5 2h7"/><path d="M14.5 16h-5"/></svg>
            {%- when 'star' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
            {%- when 'europe' -%}
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="10"/><path d="M12 2a14.5 14.5 0 0 0 0 20 14.5 14.5 0 0 0 0-20"/><path d="M2 12h20"/></svg>
          {%- endcase -%}
        </div>
        {%- if block.settings.title != blank -%}
          <h3 class="vitalys-benefits__item-title">{{ block.settings.title }}</h3>
        {%- endif -%}
        {%- if block.settings.body != blank -%}
          <p class="vitalys-benefits__item-body">{{ block.settings.body }}</p>
        {%- endif -%}
      </div>
    {%- endfor -%}
  </div>
</section>

{% schema %}
{
  "name": "VITALYS Benefits",
  "tag": "div",
  "class": "section-wrapper",
  "max_blocks": 6,
  "disabled_on": {
    "groups": ["header"]
  },
  "settings": [
    {
      "type": "text",
      "id": "heading",
      "label": "Heading",
      "default": "Por qué elegirnos"
    },
    {
      "type": "text",
      "id": "subheading",
      "label": "Subheading"
    },
    {
      "type": "color_scheme",
      "id": "color_scheme",
      "label": "Color scheme",
      "default": "scheme-1"
    },
    {
      "type": "select",
      "id": "section_width",
      "label": "Section width",
      "options": [
        { "value": "page-width", "label": "Page width" },
        { "value": "full-width", "label": "Full width" }
      ],
      "default": "page-width"
    },
    {
      "type": "range",
      "id": "padding-block-start",
      "label": "Top padding",
      "min": 0,
      "max": 120,
      "step": 8,
      "unit": "px",
      "default": 72
    },
    {
      "type": "range",
      "id": "padding-block-end",
      "label": "Bottom padding",
      "min": 0,
      "max": 120,
      "step": 8,
      "unit": "px",
      "default": 72
    }
  ],
  "blocks": [
    {
      "type": "benefit_item",
      "name": "Benefit item",
      "settings": [
        {
          "type": "select",
          "id": "icon",
          "label": "Icon",
          "options": [
            { "value": "leaf", "label": "Hoja (Leaf)" },
            { "value": "microscope", "label": "Microscopio" },
            { "value": "shield", "label": "Escudo (Shield)" },
            { "value": "check", "label": "Check" },
            { "value": "flask", "label": "Tubo de ensayo" },
            { "value": "star", "label": "Estrella" },
            { "value": "europe", "label": "Globo (Europa)" }
          ],
          "default": "check"
        },
        {
          "type": "text",
          "id": "title",
          "label": "Title",
          "default": "Ingrediente europeo certificado"
        },
        {
          "type": "textarea",
          "id": "body",
          "label": "Description",
          "default": "Trazabilidad completa desde el origen hasta la cápsula."
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "VITALYS Benefits",
      "settings": {
        "heading": "Formulados para quienes se lo toman en serio",
        "color_scheme": "scheme-1"
      },
      "blocks": [
        {
          "type": "benefit_item",
          "settings": {
            "icon": "europe",
            "title": "Ingredientes europeos certificados",
            "body": "Trazabilidad completa. Sin materias primas de origen dudoso."
          }
        },
        {
          "type": "benefit_item",
          "settings": {
            "icon": "microscope",
            "title": "Dosificación clínica exacta",
            "body": "Las cantidades que usan los estudios, no las que abaratan el producto."
          }
        },
        {
          "type": "benefit_item",
          "settings": {
            "icon": "shield",
            "title": "Sin rellenos innecesarios",
            "body": "Sin dióxido de titanio ni excipientes que no aportan nada."
          }
        }
      ]
    }
  ]
}
{% endschema %}
```

- [ ] **Step 2: Verify the file exists and has content**

```bash
wc -l /Users/cris/Desktop/shopify-belevels/sections/vitalys-benefits.liquid
```
Expected: 150+ lines

- [ ] **Step 3: Commit**

```bash
git -C /Users/cris/Desktop/shopify-belevels add sections/vitalys-benefits.liquid
git -C /Users/cris/Desktop/shopify-belevels commit -m "feat: add vitalys-benefits section — 3-col icon grid with schema"
```

---

## Task 2: Create `sections/vitalys-testimonial.liquid`

**Files:**
- Create: `sections/vitalys-testimonial.liquid`

- [ ] **Step 1: Create the section file**

Create `/Users/cris/Desktop/shopify-belevels/sections/vitalys-testimonial.liquid` with this exact content:

```liquid
<div class="section-background color-{{ section.settings.color_scheme }}"></div>
<section
  class="section section--{{ section.settings.section_width }} vitalys-testimonial color-{{ section.settings.color_scheme }}"
  style="{%- render 'spacing-style', settings: section.settings %}"
  data-section-id="{{ section.id }}"
>
  <div class="vitalys-testimonial__inner">
    {%- assign rating = section.settings.rating | plus: 0 -%}

    {%- if section.settings.photo != blank -%}
      <div class="vitalys-testimonial__photo">
        {{
          section.settings.photo
          | image_url: width: 160
          | image_tag:
            loading: 'lazy',
            width: 80,
            height: 80,
            class: 'vitalys-testimonial__avatar',
            alt: section.settings.author_name
        }}
      </div>
    {%- else -%}
      <div class="vitalys-testimonial__photo vitalys-testimonial__photo--placeholder">
        <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="8" r="4"/><path d="M20 21a8 8 0 1 0-16 0"/></svg>
      </div>
    {%- endif -%}

    <div class="vitalys-testimonial__content">
      {%- if rating > 0 -%}
        <div class="vitalys-testimonial__stars" aria-label="{{ rating }} de 5 estrellas" role="img">
          {%- for i in (1..5) -%}
            {%- if i <= rating -%}
              <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" stroke="currentColor" stroke-width="1.5" aria-hidden="true"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
            {%- else -%}
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
            {%- endif -%}
          {%- endfor -%}
        </div>
      {%- endif -%}

      {%- if section.settings.quote != blank -%}
        <blockquote class="vitalys-testimonial__quote">
          {{ section.settings.quote }}
        </blockquote>
      {%- endif -%}

      <footer class="vitalys-testimonial__author">
        {%- if section.settings.author_name != blank -%}
          <span class="vitalys-testimonial__author-name">{{ section.settings.author_name }}</span>
        {%- endif -%}
        {%- if section.settings.author_role != blank -%}
          <span class="vitalys-testimonial__author-role">{{ section.settings.author_role }}</span>
        {%- endif -%}
      </footer>
    </div>
  </div>
</section>

{% schema %}
{
  "name": "VITALYS Testimonial",
  "tag": "div",
  "class": "section-wrapper",
  "disabled_on": {
    "groups": ["header"]
  },
  "settings": [
    {
      "type": "header",
      "content": "Review content"
    },
    {
      "type": "image_picker",
      "id": "photo",
      "label": "Author photo"
    },
    {
      "type": "range",
      "id": "rating",
      "label": "Star rating",
      "min": 1,
      "max": 5,
      "step": 1,
      "default": 5
    },
    {
      "type": "textarea",
      "id": "quote",
      "label": "Review text",
      "default": "Llevo tres meses tomando el magnesio y la diferencia en la calidad del sueño es real. Sin efectos secundarios, sin promesas vacías. Por fin una marca que da lo que dice."
    },
    {
      "type": "text",
      "id": "author_name",
      "label": "Author name",
      "default": "María G."
    },
    {
      "type": "text",
      "id": "author_role",
      "label": "Role / context",
      "default": "Cliente verificada · Madrid"
    },
    {
      "type": "header",
      "content": "Layout"
    },
    {
      "type": "color_scheme",
      "id": "color_scheme",
      "label": "Color scheme",
      "default": "scheme-2"
    },
    {
      "type": "select",
      "id": "section_width",
      "label": "Section width",
      "options": [
        { "value": "page-width", "label": "Page width" },
        { "value": "full-width", "label": "Full width" }
      ],
      "default": "page-width"
    },
    {
      "type": "range",
      "id": "padding-block-start",
      "label": "Top padding",
      "min": 0,
      "max": 120,
      "step": 8,
      "unit": "px",
      "default": 80
    },
    {
      "type": "range",
      "id": "padding-block-end",
      "label": "Bottom padding",
      "min": 0,
      "max": 120,
      "step": 8,
      "unit": "px",
      "default": 80
    }
  ],
  "presets": [
    {
      "name": "VITALYS Testimonial"
    }
  ]
}
{% endschema %}
```

- [ ] **Step 2: Verify the file exists**

```bash
wc -l /Users/cris/Desktop/shopify-belevels/sections/vitalys-testimonial.liquid
```
Expected: 120+ lines

- [ ] **Step 3: Commit**

```bash
git -C /Users/cris/Desktop/shopify-belevels add sections/vitalys-testimonial.liquid
git -C /Users/cris/Desktop/shopify-belevels commit -m "feat: add vitalys-testimonial section — featured review with photo and stars"
```

---

## Task 3: Extend `assets/vitalys.css` with homepage component styles

**Files:**
- Modify: `assets/vitalys.css`

- [ ] **Step 1: Append CSS to `assets/vitalys.css`**

Read the current end of `assets/vitalys.css` to find the last line, then append exactly this content after it:

```css

/* ─── Benefits grid ────────────────────────────────────────────── */

.vitalys-benefits {
  padding-block-start: var(--padding-block-start, 72px);
  padding-block-end: var(--padding-block-end, 72px);
  padding-inline: var(--page-padding, 48px);
}

.vitalys-benefits__header {
  text-align: center;
  margin-block-end: 56px;
}

.vitalys-benefits__heading {
  font-family: var(--font-heading-family);
  font-size: clamp(28px, 4vw, 40px);
  font-weight: 400;
  letter-spacing: -0.03em;
  color: var(--vitalys-carbon);
  margin: 0 0 12px;
  line-height: 1.15;
}

.vitalys-benefits__subheading {
  font-family: var(--font-body-family);
  font-size: 16px;
  color: var(--vitalys-carbon);
  opacity: 0.65;
  margin: 0;
  max-width: 520px;
  margin-inline: auto;
  line-height: 1.6;
}

.vitalys-benefits__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 48px 40px;
}

@media screen and (max-width: 989px) {
  .vitalys-benefits__grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 36px 28px;
  }
}

@media screen and (max-width: 749px) {
  .vitalys-benefits {
    padding-inline: 20px;
  }

  .vitalys-benefits__grid {
    grid-template-columns: 1fr;
    gap: 32px;
  }

  .vitalys-benefits__header {
    margin-block-end: 36px;
  }
}

.vitalys-benefits__item {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.vitalys-benefits__icon {
  color: var(--vitalys-gold);
  width: 32px;
  height: 32px;
  flex-shrink: 0;
  margin-block-end: 4px;
}

.vitalys-benefits__icon svg {
  display: block;
}

.vitalys-benefits__item-title {
  font-family: var(--font-heading-family);
  font-size: 20px;
  font-weight: 400;
  color: var(--vitalys-carbon);
  margin: 0;
  line-height: 1.3;
  letter-spacing: -0.01em;
}

.vitalys-benefits__item-body {
  font-family: var(--font-body-family);
  font-size: 15px;
  line-height: 1.65;
  color: var(--vitalys-carbon);
  opacity: 0.72;
  margin: 0;
}

/* ─── Testimonial ───────────────────────────────────────────────── */

.vitalys-testimonial {
  padding-block-start: var(--padding-block-start, 80px);
  padding-block-end: var(--padding-block-end, 80px);
  padding-inline: var(--page-padding, 48px);
}

.vitalys-testimonial__inner {
  max-width: 720px;
  margin-inline: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 28px;
  text-align: center;
}

.vitalys-testimonial__avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  display: block;
}

.vitalys-testimonial__photo--placeholder {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: var(--vitalys-sand);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--vitalys-carbon);
  opacity: 0.5;
}

.vitalys-testimonial__stars {
  display: flex;
  gap: 3px;
  justify-content: center;
  color: var(--vitalys-gold);
}

.vitalys-testimonial__quote {
  font-family: var(--font-heading-family);
  font-size: clamp(20px, 3vw, 28px);
  font-style: italic;
  line-height: 1.45;
  color: var(--vitalys-carbon);
  margin: 0;
}

.vitalys-testimonial__quote::before {
  content: '\201C';
}

.vitalys-testimonial__quote::after {
  content: '\201D';
}

.vitalys-testimonial__author {
  display: flex;
  flex-direction: column;
  gap: 4px;
  align-items: center;
}

.vitalys-testimonial__author-name {
  font-family: var(--font-body-family);
  font-size: 13px;
  font-weight: 500;
  color: var(--vitalys-carbon);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  display: block;
}

.vitalys-testimonial__author-role {
  font-family: var(--font-body-family);
  font-size: 12px;
  color: var(--vitalys-carbon);
  opacity: 0.55;
  display: block;
}

@media screen and (max-width: 749px) {
  .vitalys-testimonial {
    padding-inline: 20px;
  }
}
```

- [ ] **Step 2: Verify CSS was appended**

```bash
grep -c "vitalys-benefits\|vitalys-testimonial" /Users/cris/Desktop/shopify-belevels/assets/vitalys.css
```
Expected: 15 or more matches

- [ ] **Step 3: Commit**

```bash
git -C /Users/cris/Desktop/shopify-belevels add assets/vitalys.css
git -C /Users/cris/Desktop/shopify-belevels commit -m "style: add benefits grid and testimonial CSS to vitalys.css"
```

---

## Task 4: Rebuild `templates/index.json` — 7-section homepage

**Files:**
- Replace: `templates/index.json`
- Modify: `sections/footer-group.json`

- [ ] **Step 1: Replace `templates/index.json` with the 7-section homepage**

Write `/Users/cris/Desktop/shopify-belevels/templates/index.json` with this exact content:

```json
{
  "sections": {
    "hero": {
      "type": "hero",
      "blocks": {
        "text-heading": {
          "type": "text",
          "settings": {
            "text": "<h1>La diferencia está en lo que no se ve.</h1>",
            "type_preset": "h1",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "wrap": "pretty"
          }
        },
        "text-sub": {
          "type": "text",
          "settings": {
            "text": "<p>Suplementos formulados con ingredientes europeos certificados y dosificación clínica exacta.</p>",
            "type_preset": "rte",
            "width": "fit-content",
            "max_width": "normal",
            "alignment": "left",
            "wrap": "pretty"
          }
        },
        "btn-discover": {
          "type": "button",
          "settings": {
            "label": "Descubrir productos",
            "link": "/collections/all",
            "style_class": "button-primary",
            "width": "fit-content"
          }
        }
      },
      "block_order": ["text-heading", "text-sub", "btn-discover"],
      "settings": {
        "color_scheme": "scheme-1",
        "media_type_1": "image",
        "media_type_2": "image",
        "stack_media_on_mobile": false,
        "custom_mobile_media": false,
        "media_type_1_mobile": "image",
        "media_type_2_mobile": "image",
        "open_in_new_tab": false,
        "content_direction": "column",
        "vertical_on_mobile": true,
        "horizontal_alignment_flex_direction_column": "flex-start",
        "vertical_alignment_flex_direction_column": "flex-end",
        "gap": 24,
        "section_width": "page-width",
        "section_height": "large",
        "toggle_overlay": false,
        "overlay_color": "#12121200",
        "overlay_style": "solid",
        "padding-block-start": 80,
        "padding-block-end": 72
      }
    },
    "trust-bar": {
      "type": "marquee",
      "blocks": {
        "ann-1": {
          "type": "text",
          "settings": {
            "text": "Fabricado en Europa · Fórmula clínica · Sin dióxido de titanio · Nutricionistas propios · +4.800 valoraciones",
            "type_preset": "custom",
            "font": "var(--font-body--family)",
            "font_size": "var(--font-size--h5)",
            "line_height": "normal",
            "letter_spacing": "normal",
            "case": "none",
            "wrap": "nowrap",
            "width": "fit-content"
          }
        }
      },
      "block_order": ["ann-1"],
      "settings": {
        "color_scheme": "scheme-2",
        "movement_direction": "normal",
        "gap_between_elements": 48,
        "padding-block-start": 20,
        "padding-block-end": 20
      }
    },
    "benefits": {
      "type": "vitalys-benefits",
      "blocks": {
        "b-1": {
          "type": "benefit_item",
          "settings": {
            "icon": "europe",
            "title": "Ingredientes europeos certificados",
            "body": "Trazabilidad completa. Sin materias primas de origen dudoso."
          }
        },
        "b-2": {
          "type": "benefit_item",
          "settings": {
            "icon": "microscope",
            "title": "Dosificación clínica exacta",
            "body": "Las cantidades que usan los estudios, no las que abaratan el producto."
          }
        },
        "b-3": {
          "type": "benefit_item",
          "settings": {
            "icon": "shield",
            "title": "Sin rellenos innecesarios",
            "body": "Sin dióxido de titanio ni excipientes que no aportan nada."
          }
        }
      },
      "block_order": ["b-1", "b-2", "b-3"],
      "settings": {
        "heading": "Formulados para quienes se lo toman en serio",
        "color_scheme": "scheme-1",
        "section_width": "page-width",
        "padding-block-start": 72,
        "padding-block-end": 72
      }
    },
    "bestsellers": {
      "type": "product-list",
      "blocks": {
        "static-header": {
          "type": "_product-list-content",
          "static": true,
          "settings": {
            "content_direction": "row",
            "horizontal_alignment": "space-between",
            "vertical_alignment": "flex-end",
            "align_baseline": true,
            "horizontal_alignment_flex_direction_column": "flex-start",
            "gap": 12,
            "width": "fill",
            "height": "fit",
            "inherit_color_scheme": true,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {
            "bestsellers-title": {
              "type": "_product-list-text",
              "settings": {
                "text": "<h2>Los más vendidos</h2>",
                "type_preset": "h2",
                "width": "fit-content",
                "alignment": "left",
                "wrap": "pretty"
              }
            }
          },
          "block_order": ["bestsellers-title"]
        },
        "static-product-card": {
          "type": "_product-card",
          "static": true,
          "settings": {
            "product_card_gap": 8,
            "inherit_color_scheme": true,
            "border": "none",
            "border_radius": 0,
            "padding-block-start": 0,
            "padding-block-end": 0,
            "padding-inline-start": 0,
            "padding-inline-end": 0
          },
          "blocks": {
            "product-card-gallery": {
              "type": "_product-card-gallery",
              "static": true,
              "settings": {
                "image_ratio": "adapt",
                "border": "none",
                "border_radius": 0
              }
            },
            "product-title": {
              "type": "product-title",
              "settings": {
                "width": "100%",
                "alignment": "left",
                "type_preset": "rte",
                "padding-block-start": 8,
                "padding-block-end": 0
              }
            },
            "price": {
              "type": "price",
              "settings": {
                "show_sale_price_first": true,
                "type_preset": "h6",
                "width": "100%",
                "alignment": "left"
              }
            },
            "buy-btn": {
              "type": "buy-buttons",
              "settings": {
                "show_dynamic_checkout": false,
                "show_gift_card_recipient": false
              }
            }
          },
          "block_order": ["product-card-gallery", "product-title", "price", "buy-btn"]
        }
      },
      "settings": {
        "collection": "all",
        "color_scheme": "scheme-1",
        "layout_type": "grid",
        "max_products": 3,
        "columns": 3,
        "mobile_columns": "1",
        "columns_gap": 24,
        "rows_gap": 32,
        "section_width": "page-width",
        "horizontal_alignment": "flex-start",
        "gap": 32,
        "padding-block-start": 64,
        "padding-block-end": 64
      }
    },
    "pillars": {
      "type": "section",
      "blocks": {
        "heading-block": {
          "type": "text",
          "settings": {
            "text": "<h2>Por qué VITALYS</h2>",
            "type_preset": "h2",
            "width": "fill",
            "alignment": "center",
            "wrap": "pretty"
          }
        },
        "col-1": {
          "type": "group",
          "settings": {
            "content_direction": "column",
            "horizontal_alignment_flex_direction_column": "flex-start",
            "vertical_alignment_flex_direction_column": "flex-start",
            "gap": 12,
            "width": "fill",
            "height": "fit",
            "inherit_color_scheme": true,
            "padding-block-start": 24,
            "padding-block-end": 24,
            "padding-inline-start": 16,
            "padding-inline-end": 16
          },
          "blocks": {
            "col-1-title": {
              "type": "text",
              "settings": {
                "text": "<h4>Ingredientes europeos certificados</h4>",
                "type_preset": "h4",
                "width": "fill",
                "alignment": "left",
                "wrap": "pretty"
              }
            },
            "col-1-text": {
              "type": "text",
              "settings": {
                "text": "<p>Trazabilidad completa. Sin materias primas de origen dudoso.</p>",
                "type_preset": "rte",
                "width": "fill",
                "alignment": "left"
              }
            }
          },
          "block_order": ["col-1-title", "col-1-text"]
        },
        "col-2": {
          "type": "group",
          "settings": {
            "content_direction": "column",
            "horizontal_alignment_flex_direction_column": "flex-start",
            "vertical_alignment_flex_direction_column": "flex-start",
            "gap": 12,
            "width": "fill",
            "height": "fit",
            "inherit_color_scheme": true,
            "padding-block-start": 24,
            "padding-block-end": 24,
            "padding-inline-start": 16,
            "padding-inline-end": 16
          },
          "blocks": {
            "col-2-title": {
              "type": "text",
              "settings": {
                "text": "<h4>Dosificación clínica exacta</h4>",
                "type_preset": "h4",
                "width": "fill",
                "alignment": "left"
              }
            },
            "col-2-text": {
              "type": "text",
              "settings": {
                "text": "<p>Las cantidades que usan los estudios, no las que abaratan el producto.</p>",
                "type_preset": "rte",
                "width": "fill",
                "alignment": "left"
              }
            }
          },
          "block_order": ["col-2-title", "col-2-text"]
        },
        "col-3": {
          "type": "group",
          "settings": {
            "content_direction": "column",
            "horizontal_alignment_flex_direction_column": "flex-start",
            "vertical_alignment_flex_direction_column": "flex-start",
            "gap": 12,
            "width": "fill",
            "height": "fit",
            "inherit_color_scheme": true,
            "padding-block-start": 24,
            "padding-block-end": 24,
            "padding-inline-start": 16,
            "padding-inline-end": 16
          },
          "blocks": {
            "col-3-title": {
              "type": "text",
              "settings": {
                "text": "<h4>Fórmulas propias</h4>",
                "type_preset": "h4",
                "width": "fill",
                "alignment": "left"
              }
            },
            "col-3-text": {
              "type": "text",
              "settings": {
                "text": "<p>Sin copiar. Sin fórmulas propietarias que oculten cantidades.</p>",
                "type_preset": "rte",
                "width": "fill",
                "alignment": "left"
              }
            }
          },
          "block_order": ["col-3-title", "col-3-text"]
        },
        "col-4": {
          "type": "group",
          "settings": {
            "content_direction": "column",
            "horizontal_alignment_flex_direction_column": "flex-start",
            "vertical_alignment_flex_direction_column": "flex-start",
            "gap": 12,
            "width": "fill",
            "height": "fit",
            "inherit_color_scheme": true,
            "padding-block-start": 24,
            "padding-block-end": 24,
            "padding-inline-start": 16,
            "padding-inline-end": 16
          },
          "blocks": {
            "col-4-title": {
              "type": "text",
              "settings": {
                "text": "<h4>Packaging sin rellenos</h4>",
                "type_preset": "h4",
                "width": "fill",
                "alignment": "left"
              }
            },
            "col-4-text": {
              "type": "text",
              "settings": {
                "text": "<p>Sin dióxido de titanio ni rellenos innecesarios.</p>",
                "type_preset": "rte",
                "width": "fill",
                "alignment": "left"
              }
            }
          },
          "block_order": ["col-4-title", "col-4-text"]
        }
      },
      "block_order": ["heading-block", "col-1", "col-2", "col-3", "col-4"],
      "settings": {
        "color_scheme": "scheme-2",
        "content_direction": "row",
        "vertical_on_mobile": true,
        "horizontal_alignment": "space-between",
        "vertical_alignment": "flex-start",
        "horizontal_alignment_flex_direction_column": "flex-start",
        "gap": 24,
        "section_width": "page-width",
        "section_height": "",
        "padding-block-start": 64,
        "padding-block-end": 64
      }
    },
    "testimonial": {
      "type": "vitalys-testimonial",
      "settings": {
        "rating": 5,
        "quote": "Llevo tres meses tomando el magnesio y la diferencia en la calidad del sueño es real. Sin efectos secundarios, sin promesas vacías. Por fin una marca que da lo que dice.",
        "author_name": "María G.",
        "author_role": "Cliente verificada · Madrid",
        "color_scheme": "scheme-2",
        "section_width": "page-width",
        "padding-block-start": 80,
        "padding-block-end": 80
      }
    },
    "faq": {
      "type": "section",
      "blocks": {
        "faq-heading": {
          "type": "text",
          "settings": {
            "text": "<h2>Preguntas frecuentes</h2>",
            "type_preset": "h2",
            "width": "fill",
            "alignment": "center",
            "wrap": "pretty"
          }
        },
        "faq-accordion": {
          "type": "accordion",
          "settings": {
            "width": "fill",
            "max_width": "normal",
            "padding-block-start": 0,
            "padding-block-end": 0
          },
          "blocks": {
            "faq-row-1": {
              "type": "_accordion-row",
              "settings": {
                "heading": "¿Qué diferencia a VITALYS de otras marcas?",
                "heading_preset": "h5"
              },
              "blocks": {
                "faq-row-1-body": {
                  "type": "text",
                  "settings": {
                    "text": "<p>Publicamos dosis exactas de cada ingrediente. Sin fórmulas propietarias que oculten cantidades. Todos nuestros ingredientes tienen origen europeo certificado con trazabilidad completa.</p>",
                    "type_preset": "rte",
                    "width": "fill",
                    "alignment": "left"
                  }
                }
              },
              "block_order": ["faq-row-1-body"]
            },
            "faq-row-2": {
              "type": "_accordion-row",
              "settings": {
                "heading": "¿Son aptos para veganos?",
                "heading_preset": "h5"
              },
              "blocks": {
                "faq-row-2-body": {
                  "type": "text",
                  "settings": {
                    "text": "<p>Sí. Todos nuestros productos están formulados sin ingredientes de origen animal y son aptos para veganos.</p>",
                    "type_preset": "rte",
                    "width": "fill",
                    "alignment": "left"
                  }
                }
              },
              "block_order": ["faq-row-2-body"]
            },
            "faq-row-3": {
              "type": "_accordion-row",
              "settings": {
                "heading": "¿Cuánto tiempo hasta notar efecto?",
                "heading_preset": "h5"
              },
              "blocks": {
                "faq-row-3-body": {
                  "type": "text",
                  "settings": {
                    "text": "<p>Los resultados varían según el producto y la persona. Como guía general, espera entre 2 y 4 semanas de uso consistente para empezar a notar los efectos.</p>",
                    "type_preset": "rte",
                    "width": "fill",
                    "alignment": "left"
                  }
                }
              },
              "block_order": ["faq-row-3-body"]
            },
            "faq-row-4": {
              "type": "_accordion-row",
              "settings": {
                "heading": "¿Puedo combinar varios productos?",
                "heading_preset": "h5"
              },
              "blocks": {
                "faq-row-4-body": {
                  "type": "text",
                  "settings": {
                    "text": "<p>La mayoría de nuestros productos son compatibles entre sí. Consulta la sección de ingredientes de cada producto para verificar interacciones específicas, o escríbenos directamente.</p>",
                    "type_preset": "rte",
                    "width": "fill",
                    "alignment": "left"
                  }
                }
              },
              "block_order": ["faq-row-4-body"]
            }
          },
          "block_order": ["faq-row-1", "faq-row-2", "faq-row-3", "faq-row-4"]
        }
      },
      "block_order": ["faq-heading", "faq-accordion"],
      "settings": {
        "color_scheme": "scheme-1",
        "content_direction": "column",
        "vertical_on_mobile": true,
        "horizontal_alignment": "center",
        "vertical_alignment": "center",
        "horizontal_alignment_flex_direction_column": "center",
        "gap": 32,
        "section_width": "page-width",
        "section_height": "",
        "padding-block-start": 72,
        "padding-block-end": 72
      }
    }
  },
  "order": ["hero", "trust-bar", "benefits", "bestsellers", "pillars", "testimonial", "faq"]
}
```

- [ ] **Step 2: Validate JSON**

```bash
python3 -c "import json; json.load(open('/Users/cris/Desktop/shopify-belevels/templates/index.json')); print('JSON valid')"
```
Expected output: `JSON valid`

- [ ] **Step 3: Update `sections/footer-group.json`** — change footer to VITALYS Carbon scheme with brand copy

In `sections/footer-group.json`, find the `footer_m9NzUG` section and update:
1. `settings.color_scheme` → `"scheme-5"` (Carbon dark)
2. `text_LWt8Pz.settings.text` → `"<h3>Sin spam. Solo ciencia.</h3>"`
3. `text_f9CFLH.settings.text` → `"<p>Novedades de formulación, estudios y descuentos para suscriptores.</p>"`
4. `footer_utilities_jLGE8U.settings.color_scheme` → `"scheme-5"`

Read the file first, then make targeted edits to only those 4 values.

- [ ] **Step 4: Verify footer JSON is valid**

```bash
python3 -c "import json; data=open('/Users/cris/Desktop/shopify-belevels/sections/footer-group.json').read(); json.loads(data[data.index('{'):]) ; print('Footer JSON valid')"
```
Expected: `Footer JSON valid`

- [ ] **Step 5: Commit both files**

```bash
git -C /Users/cris/Desktop/shopify-belevels add templates/index.json sections/footer-group.json
git -C /Users/cris/Desktop/shopify-belevels commit -m "feat: rebuild homepage — 7 VITALYS sections + Carbon footer"
```

---

## Self-Review

### Spec coverage

| User requirement | Task that covers it |
|-----------------|---------------------|
| Hero: headline Playfair, subheadline, dark CTA, Cream bg | Task 4 → `hero` section with `text-sub` block added |
| Trust indicators below hero | Task 4 → `trust-bar` marquee (scheme-2, Sand) |
| Benefits: 3 columns, linear icons | Task 1 → `vitalys-benefits.liquid` + Task 3 → CSS grid |
| Products: grid of 3, price + button | Task 4 → `bestsellers` with `buy-buttons` block, `max_products: 3` |
| Trust block: ingredients, certs, dosage | Task 4 → `pillars` section (4 columns, scheme-2) |
| Review: photo and name | Task 2 → `vitalys-testimonial.liquid` + Task 3 → CSS |
| FAQ with accordion | Task 4 → `faq` section using `section.liquid` + accordion blocks |
| Footer minimal | Task 4 → `footer-group.json` with Carbon scheme + VITALYS copy |

### Placeholder scan
No TBD, TODO, or incomplete sections found. All code blocks are complete.

### Type consistency
- `vitalys-benefits` section type used in `benefits` block in Task 4 matches the filename created in Task 1 (`vitalys-benefits.liquid` → type `"vitalys-benefits"`) ✓
- `vitalys-testimonial` section type in Task 4 matches filename from Task 2 ✓
- Block type `benefit_item` in Task 4 matches schema in Task 1 ✓
- `_accordion-row` block type in Task 4 matches the pattern proven in `templates/product.json` ✓
