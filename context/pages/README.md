# Jerarquía de páginas

Un archivo Markdown por página o tipo de página: objetivo, orden de secciones, contenido, CTAs y pendientes.

## Páginas documentadas

- [Home](home.md)
- [Colección](collection.md)
- [Producto](product.md)
- [Carrito](cart.md)
- [Navegación global](navigation.md)

Añade otras cuando se definan (`search.md`, `about.md`, `subscription.md`, `faq.md`…). Crear el archivo no las añade al alcance.

Si varios productos tienen estructuras distintas, documenta `product-<variante>.md`; si comparten estructura, una sola jerarquía con sus diferencias.

## Plantilla para una nueva página

```markdown
# Nombre de página — {{MARCA}}

## Objetivo de la página

Qué necesita comprender o hacer el visitante.

Estado: Propuesta / Definida por el usuario / Pendiente de revisión.

## Jerarquía

### 1. Nombre de sección

Objetivo:
Título:
Texto:
Contenido:
CTA principal:
CTA secundario:
Destino o comportamiento:
Referencia aplicable: (ficha de REFERENCES.md)
Activos necesarios:
Pendientes:

### 2. Nombre de sección

Repetir los campos relevantes.

## Notas de estructura

Qué es global y qué pertenece a esta página. Variaciones para móvil.
```

## Relación con los otros documentos

- `../PROJECT.md`: negocio, público, oferta y objetivos.
- `../DESIGN.md`: apariencia y comportamiento visual.
- `../references/REFERENCES.md`: patrones de referencia.
- `../DECISIONS.md`: cambios de rumbo.

Antes de implementar una página, lee su jerarquía junto con el contexto general y resuelve las contradicciones de la parte afectada.
