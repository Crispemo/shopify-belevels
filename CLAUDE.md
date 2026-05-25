# VITALYS — Claude Code Instructions

Tienda Shopify de suplementos premium europeos. Inspirada en belevels.com. Cada decisión técnica y de diseño se rige por el PRD en `docs/VITALYS-PRD.md`.

---

## Proyecto

**Marca:** VITALYS — suplementos formulados con ingredientes europeos certificados, dosificación clínica, sin rellenos.  
**Tagline:** "La diferencia está en lo que no se ve."  
**Público:** Profesionales 28–45 años. Exigen datos, no promesas.  
**Referencia visual:** belevels.com

---

## Stack

| Capa | Tecnología |
|------|-----------|
| Plataforma | Shopify |
| Tema base | **Dawn** — no reemplazar, extender |
| Plantillas | Shopify Liquid + JSON templates |
| CSS de marca | `assets/vitalys.css` |
| Config de tema | `config/settings_data.json` |
| Control de versiones | GitHub, rama `main` |

---

## Archivos clave

- `docs/VITALYS-PRD.md` — fuente de verdad para diseño, copy y componentes
- `VITALYS-brand.md` — identidad de marca: paleta, tipografía, tono
- `assets/vitalys.css` — tokens CSS (`--vitalys-cream`, `--vitalys-carbon`, etc.) y clases utilitarias
- `config/settings_data.json` — paleta y tipografía del tema (schemes 1–6)
- `layout/theme.liquid` — carga `vitalys.css` antes de `</head>`
- `templates/index.json` — homepage (7 secciones)
- `templates/product.json` — página de producto (3 secciones)

---

## Reglas de desarrollo

### Liquid y estructura Dawn
- Trabajar siempre en **Liquid** — no introducir JS frameworks, no Vue, no React.
- No modificar la estructura interna de las secciones Dawn existentes. Extender via JSON templates y `vitalys.css`.
- Nuevas secciones: crear en `sections/` siguiendo el patrón Dawn (schema al final del archivo, bloques con `{% schema %}`).
- Usar `{{ 'vitalys.css' | asset_url }}` — nunca rutas hardcodeadas.

### Sistema de diseño
- **Antes de cualquier decisión visual**, consultar `docs/VITALYS-PRD.md`.
- Colores: usar **siempre** los tokens CSS (`--vitalys-cream`, `--vitalys-carbon`, `--vitalys-gold`, `--vitalys-sand`, `--vitalys-forest`) o los color schemes de Shopify (`scheme-1` a `scheme-6`). Nunca hardcodear hex en secciones o snippets.
- Tipografía: Playfair Display para H1/H2/H3. DM Sans para body, UI, labels. No introducir otras fuentes.
- Radios: 4px en todo — botones, badges, inputs, cards. No usar valores distintos sin justificación en el PRD.
- Imágenes de producto: fondo siempre Cream (`#F7F5F0`), sin sombras.

### Copy
- Idioma: **español** en todo el contenido visible.
- Tono: preciso, contenido, sin hype. Ver ejemplos en `VITALYS-brand.md` sección "Tono de comunicación".
- Nunca escribir: urgencia artificial, hipérboles sin respaldo, emojis en web, "consulta a tu médico" como única respuesta.

### JSON templates
- Usar solo `type` de sección que exista en `sections/` — verificar antes de escribir.
- Usar solo `type` de bloque que exista en el schema de la sección correspondiente.
- Verificar JSON válido tras cada cambio: `python3 -c "import json; json.load(open('templates/ARCHIVO.json'))"`.

### Git
- Un commit por tarea lógica. Prefijo `feat:` para nuevo contenido, `fix:` para correcciones, `style:` para ajustes visuales sin cambio de funcionalidad.
- No forzar push a `main` sin confirmación explícita del usuario.

---

## Lo que VITALYS no es

No es una tienda de gym. No tiene contadores de stock falsos, banners rojos de oferta, ni CTAs agresivos. Si algo suena a hype, está mal.

Test rápido: ¿Lo aprobaría una nutricionista clínica seria? Si no, no va.
