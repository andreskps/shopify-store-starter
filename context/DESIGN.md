# DESIGN.md — Sistema de diseño {{MARCA}}

> Los valores de este documento son los **valores iniciales** de marca; las secciones del tema deben permitir ajustarlos desde el editor. Marca cada decisión como Confirmado / Propuesta / Pendiente. Los cambios de dirección se registran en `DECISIONS.md` y se reflejan aquí, en la sección correspondiente.

## 1. Dirección visual

- **Concepto creativo:**
- **Sensaciones que debe transmitir:**
- **Traducción a decisiones observables:** (p. ej. "energético" → contraste alto, tipografía bold, color saturado en CTAs)
- **Referencias base:** enlaces a fichas de `references/REFERENCES.md`.

## 2. Colores

### Paleta base
| Token | Valor | Uso |
|---|---|---|
| `--{{PREFIJO}}-color-ink` | | Texto principal |
| `--{{PREFIJO}}-color-bg` | | Fondo |
| `--{{PREFIJO}}-color-accent` | | CTA / acento |

### Colores por línea / categoría (si aplica)
### Reglas de combinación
Combinaciones permitidas con su contraste verificado (WCAG AA mínimo para texto).

## 3. Tipografía

### Familias
Archivo y licencia en `brand/fonts/`. Se cargan mediante los ajustes globales del tema, nunca hardcodeadas por componente.
### Jerarquía tipográfica
| Nivel | Desktop | Móvil | Peso | Uso |
|---|---|---|---|---|
| H1 | | | | |
| H2 | | | | |
| Cuerpo | | | | |
| Botón | | | | |

### Reglas tipográficas

## 4. Layout y espaciado

- Ancho máximo de página:
- Escala de espaciado:
### Grid
### Reglas de composición

## 5. Componentes

### Botones
Primario, secundario, terciario: fondo, texto, borde, radio, alto mínimo, estados (hover, focus, disabled).
### Product cards
### Selector de cantidad
### Opciones de compra (variantes, packs, suscripción)
### Inputs y selects
### Drawers y modals
### Radios (tokens de forma)
| Token | Valor | Uso |
|---|---|---|
| `--{{PREFIJO}}-radius-card` | | |
| `--{{PREFIJO}}-radius-button` | | |
| `--{{PREFIJO}}-radius-control` | | |
| `--{{PREFIJO}}-radius-detail` | | |
| `--{{PREFIJO}}-radius-pill` | | |

## 6. Fotografía y contenido visual

### Fotografía de producto
### Fotografía lifestyle
### Fondos
### Encuadres y proporciones
### Tratamiento de imágenes

## 7. Iconografía

Librería o set propio, grosor, tamaño, uso con texto.

## 8. Responsive

### Mobile
### Tablet
### Desktop

## 9. Animaciones e interacciones

Duraciones, curvas, qué se anima y qué no. Siempre con alternativa para `prefers-reduced-motion`.

## 10. Reglas visuales obligatorias

### Hacer
### No hacer

## 11. Implementación en Shopify

- Dónde viven los tokens (snippet de tokens, settings del tema).
- Qué se configura con color schemes del tema y qué con settings de sección.
### Principio técnico

## 12. Referencias y validación

- Combinaciones de contraste verificadas:
- Pruebas en 320 px, 390 px, 768 px, 1440 px:
- Pendientes visuales:
