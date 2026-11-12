# Prompts por etapa

Copia y pega en el agente. Sustituye lo que está entre `< >`.

## 1. Intake de materiales

> Vamos a preparar esta tienda sin desarrollar todavía. Revisa los materiales de `context/brand/` y los que te comparta (<URL web, redes, catálogo>). Extrae la información confirmada y hazme preguntas por bloques para completar `context/PROJECT.md`. Distingue hechos, propuestas y pendientes, y dame la lista de materiales que faltan.

## 2. Completar PROJECT.md

> Completa `context/PROJECT.md` sección por sección (información general, concepto, público, personalidad, voz, oferta, competencia, objetivos, restricciones). Hazme máximo 5 preguntas por bloque. Marca cada dato como Confirmado, Propuesta, Hipótesis o Pendiente por definir. No inventes cifras, claims ni reseñas.

## 3a. Añadir una referencia web

> Analiza esta referencia: <URL>. Me interesa <componente o página: hero, selector de variantes, carrito…> porque <razón>. Revísala con Playwright en escritorio (1440 px) y móvil (390 px), verifica la interacción, guarda capturas en `context/references/visual/<área>/` y añade la ficha en `REFERENCES.md`: qué patrón sirve, qué problema resuelve, comportamiento móvil, adaptación a nuestra marca según PROJECT.md y qué evitar. Señala lo que no puedas verificar.

## 3b. Añadir una referencia en imagen

> Añadí `context/references/visual/<área>/<archivo>`. Me interesa <qué>. Inspecciónala, documenta el patrón en `REFERENCES.md` y adáptalo a PROJECT.md. Deja claro que una imagen no demuestra interacción ni comportamiento móvil.

## 3c. Revisar todas las referencias

> Analiza las imágenes de `context/references/visual/` y las URLs de `REFERENCES.md`. Documenta qué patrones nos sirven, qué problema resuelven y cómo adaptarlos a PROJECT.md. Detecta contradicciones entre referencias y propón cuál prevalece.

## 4. Design system

> A partir de PROJECT.md, REFERENCES.md y `context/brand/`, propón el sistema visual para `context/DESIGN.md`: concepto, paleta con valores y usos, tipografía y escala, fotografía, layout, componentes (botones, cards, inputs, drawers), iconografía, responsive, movimiento, reglas y tokens para Shopify. Explica las decisiones principales, verifica contraste de las combinaciones y distingue lo confirmado de lo que necesita definición. Todavía no modifiques el tema.

## 5. Adaptar AGENTS.md

> Adapta AGENTS.md a esta tienda usando PROJECT.md, DESIGN.md, REFERENCES.md y la arquitectura real del repositorio. Reemplaza todos los `{{PLACEHOLDER}}`, verifica la versión del tema en `config/settings_schema.json` y el dominio/tema con Shopify CLI. Conserva las reglas reutilizables. No copies datos ni permisos de otra marca; marca como pendiente lo que no esté confirmado. No desarrolles componentes todavía.

## 6a. Primera versión

> Lee AGENTS.md, PROJECT.md, DESIGN.md y REFERENCES.md. Revisa la arquitectura del tema sin modificar archivos. Propón la primera versión: páginas, secciones, contenido pendiente y qué configurar, adaptar, crear o posponer.

## 6b. Documentar una página

> Documenta `context/pages/<página>.md` con la plantilla de `context/pages/README.md`: objetivo, jerarquía de secciones, títulos, textos, CTAs, destinos, activos necesarios y pendientes. Usa la voz de PROJECT.md y las referencias aplicables. Pregúntame lo que no esté definido.

## 7. Revisión de preparación

> Revisa el checklist "Listo para desarrollo" del README contra los documentos de `context/`. Dime qué está completo, qué falta y qué pendientes bloquean identidad, estructura o compra.

## 8. Implementar un bloque

> Implementa <sección> de `context/pages/<página>.md` siguiendo AGENTS.md y DESIGN.md. Todo editable desde el editor, prefijo del proyecto, sin `!important`. Verifica en Playwright escritorio y móvil (incluido 320 px), ejecuta Theme Check e informa qué no pudiste comprobar.

## Registrar un cambio de rumbo

> Cambiamos <decisión>. Regístralo en `context/DECISIONS.md` con fecha y estado, actualiza la sección afectada de <documento> y dime qué partes del tema quedan desalineadas.
