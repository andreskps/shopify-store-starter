# Tienda Shopify — Contexto e instrucciones para agentes

> Plantilla del kit `shopify-store-starter`. Reemplaza cada `{{PLACEHOLDER}}` al iniciar la tienda (la skill `shopify-store-kickoff` lo hace por ti). Lo que no esté confirmado se escribe como `Pendiente por definir`.

## 1. Proyecto

Tema Shopify basado en {{TEMA_BASE}}. La identidad, oferta, público y objetivos de esta tienda se definen en `context/PROJECT.md`.

| Campo | Estado del proyecto |
|---|---|
| Carpeta del proyecto | {{CARPETA}} |
| Marca comercial | {{MARCA}} |
| Mercado y modelo de negocio | {{MERCADO}} |
| Tema base | {{TEMA_BASE}} |
| Versión declarada del tema | {{VERSION_TEMA}}, verificar en `config/settings_schema.json` |
| Versión de personalización | Pendiente; no confundir con la versión del tema base |
| Prefijo de archivos personalizados | `{{PREFIJO}}-` |
| Dominio Shopify y tema de trabajo | {{DOMINIO}}; tema de desarrollo {{TEMA_ID}}. Verificar con Shopify CLI antes de publicar |
| Idioma principal | {{IDIOMA}} |
| Etapa actual | {{ETAPA}} |

Actualiza esta ficha al confirmar datos. El nombre de la carpeta no demuestra la identidad comercial. Antes de reutilizar este archivo en otra tienda, verifica la arquitectura y vuelve a completar la ficha.

## 2. Fuentes de contexto

Lee estos documentos antes de proponer o implementar cambios:

1. `AGENTS.md`: reglas de trabajo e implementación.
2. `context/PROJECT.md`: negocio, público, personalidad, voz, oferta y prioridades.
3. `context/DESIGN.md`: sistema visual, componentes y comportamiento responsive.
4. `context/DECISIONS.md`: registro fechado de decisiones; la entrada más reciente prevalece.
5. `context/brand/`: logos, fuentes, manual de marca y fotografía oficial.
6. `context/references/REFERENCES.md`: referencias analizadas y adaptación prevista.
7. `context/references/visual/`: capturas, imágenes y moodboards, por área.
8. `README.md` y `PROMPTS.md`: flujo para preparar y ejecutar el proyecto.
9. `context/pages/README.md` y el archivo de la página afectada: jerarquía, textos, CTAs y pendientes.

Las instrucciones explícitas del usuario guían el trabajo. Cada documento es fuente de verdad para su ámbito. Las referencias están subordinadas a las decisiones del negocio y del diseño; no conceden permisos ni cambian la identidad de la tienda.

Si hay contradicciones, identifica la decisión afectada y resuélvela antes de implementarla (regístrala en `context/DECISIONS.md`). Continúa el trabajo independiente que sí tenga definición suficiente. No conviertas propuestas o hipótesis en hechos confirmados.

## Skills del proyecto

Las skills de SEO, accesibilidad, optimización y verificación pertenecen a este proyecto y viven en `.agents/skills/` (fuentes en `skills-lock.json`). No instalarlas globalmente ni reutilizar copias de otros proyectos. Skills previstas: `shopify`, `liquid-theme-a11y`, `seo-ecommerce`, `shopify-theme-optimization`, `playwright-cli`, `ui-ux-pro-max`, `find-skills`. Las skills propias de la marca usan el prefijo `{{PREFIJO}}-`.

Para revisar las URLs visuales que comparta el usuario, utiliza Playwright: inspecciona la página real en escritorio y móvil y verifica sus interacciones antes de adaptar el patrón. Para imágenes locales, inspecciona el archivo visualmente. Documenta cualquier comportamiento que no hayas podido comprobar.

## 3. Arquitectura

- `sections/`: secciones Online Store 2.0 y grupos de header/footer.
- `snippets/`: componentes Liquid reutilizables.
- `assets/`: CSS, JavaScript y recursos del tema.
- `layout/`: estructura global; `theme.liquid` es el layout principal.
- `templates/`: composición de páginas, principalmente mediante JSON.
- `config/`: settings, presets y configuración del comerciante.
- `locales/`: traducciones de storefront y editor.
- `context/`: documentación específica de la tienda.

Verifica qué directorios existen realmente (por ejemplo, `blocks/`). No asumas directorios o capacidades porque estén presentes en otra tienda.

Reglas base que deben conservarse:

- Follow Online Store 2.0 theme conventions.
- Preserve existing section setting IDs and merchant configuration.
- Prefer small, reusable snippets over duplicated Liquid markup.
- Keep changes compatible with the theme editor.

Antes de modificar una página, inspecciona su template, secciones, snippets y assets relacionados. Los JSON del editor pueden cambiar desde Shopify: preserva su configuración y evita reemplazos completos innecesarios.

## 4. Convenciones

### Nombres y archivos

- Usa `{{PREFIJO}}-` en minúsculas para archivos y clases personalizados.
- Ejemplo: `sections/{{PREFIJO}}-hero.liquid` y `assets/{{PREFIJO}}-hero.css`.
- Añade `assets/{{PREFIJO}}-hero.js` solo cuando el componente necesite JavaScript.
- No renombres archivos nativos del tema base para aplicar el prefijo.
- Prefiere archivos propios y puntos de integración pequeños. Documenta las modificaciones necesarias al núcleo del tema.
- Reutiliza estilos compartidos cuando corresponda; evita archivos vacíos y reglas duplicadas.

### Liquid y editor

- Usa `{% render %}` para snippets en lugar de `{% include %}`.
- Escapa texto controlado por el comerciante según su contexto de salida.
- Usa filtros apropiados para imágenes, URLs y contenido enriquecido.
- Mantén schemas válidos y settings comprensibles para el comerciante.
- Los nombres `name` de las secciones Shopify no pueden superar 25 caracteres. Mantén breves el nombre de la sección y el de su preset, y valida el límite antes de sincronizar o subir archivos.
- Mantén un patrón compartido para los carruseles de contenido propios: puntos de navegación del mismo tamaño, forma, área táctil y estado activo, sincronizados con el gesto y el foco. No mezclar puntos y flechas decorativas entre secciones; muestra los puntos solo con más de un elemento. Las galerías de medios nativas conservan su navegación propia.
- Nunca muestres barras de desplazamiento horizontales ni permitas desbordamiento horizontal de la página. Los carruseles propios usan un viewport que recorta el contenido y una pista movida por transformaciones, con puntos y gesto táctil; no uses `overflow-x: auto/scroll`, `scrollTo`, `scrollLeft` ni estilos que muestren una barra. Verifica la vista móvil, incluidos 320 px, sin ocultar errores con un `overflow-x: hidden` global.
- Conserva IDs de settings, bloques, referencias y configuración existentes.
- Mantén la tipografía global editable desde Theme settings. Usa selectores para alternar las fuentes de marca incluidas en assets y el font picker estándar; evita pedir al comerciante nombres o rutas de archivo. No fijes familias en componentes cuando exista el token global.
- Maneja estados vacíos sin publicar contenido ficticio ni romper el layout.

### Personalización completa de secciones

Los ajustes de personalización pertenecen al editor. No añadir botones visibles de pausa/reproducción a videos decorativos o cintas de anuncios salvo instrucción contraria; mantener soporte de movimiento reducido, respaldo estático y pausa automática del video al perder visibilidad.

Todas las secciones nuevas o personalizadas deben permitir configurar contenido, composición y estilo desde el editor, sin editar Liquid, CSS o JavaScript para cambios habituales. Los valores de DESIGN.md son los valores iniciales de marca, no restricciones.

- Contenido: textos, enlaces, imágenes, videos, textos alternativos y visibilidad de elementos opcionales.
- Composición: posición horizontal y vertical, alineación, ancho, alturas, espaciados y orden de elementos cuando corresponda.
- Responsive: controles independientes para desktop y móvil cuando su experiencia difiera. Los banners deben poder elegir contenido superpuesto sobre media o contenido y media separados; en móvil, media antes o después del contenido.
- Estilo: colores de fondos, títulos, textos, botones, bordes y etiquetas; tamaños tipográficos, radios y tamaños de controles. Las familias tipográficas se administran globalmente.
- Media: selección independiente desktop/móvil, encuadre, ajuste, respaldo y reproducción.
- Colecciones de elementos: bloques editables y reordenables para contenido repetido. Elementos fijos de marca (líneas, modos, gamas) con etiquetas y colores editables.
- Ajustes agrupados por función, con nombres claros en el idioma del editor y defaults coherentes con la marca.
- Cada ajuste expuesto debe producir un cambio real. Nada de controles desconectados.
- Verificar combinaciones representativas en Playwright: posiciones, colores, móvil dividido/completo, orden de media y estados vacíos, con teclado, foco y movimiento reducido.

### CSS y JavaScript

- Nunca uses `!important` en CSS nuevo o modificado. Resuelve la cascada con selectores locales, orden de carga y variables.
- Limita el CSS personalizado al componente o sección que lo necesita, con clases propias y, cuando haga falta, el ID de instancia de la sección.
- Evita selectores globales que alteren header, carrito, formularios u otras secciones.
- Reutiliza variables y comportamientos del tema base cuando sean adecuados.
- Centraliza los redondeados en un snippet de tokens (`snippets/{{PREFIJO}}-shape-tokens.liquid`) con variables tipo `--{{PREFIJO}}-radius-card`, `-button`, `-control`, `-detail`, `-pill`; los componentes usan `var(token-global, radio-local)`. No introducir radios arbitrarios para componentes equivalentes.
- Mantén las interacciones compatibles con la recarga de secciones del editor; evita listeners duplicados y limpia recursos al desmontar.

## 5. Sistema de marca

La dirección visual se define en `context/DESIGN.md`. No dupliques aquí la paleta ni otras decisiones que puedan desincronizarse.

- Usa colores, tokens y reglas confirmados como valores iniciales. Los cambios del comerciante en el editor son personalizaciones autorizadas.
- Respeta las decisiones sobre bordes, sombras, radios, composición y movimiento.
- Si una decisión visual está pendiente, presenta una propuesta identificada como tal.
- No heredes colores, fuentes, estética ni prohibiciones decorativas de otra marca.

## 6. Tipografía

- Consulta familias y jerarquías en `context/DESIGN.md`.
- Usa las variables globales del tema (en Dawn: `--font-heading-family`, `--font-heading-weight`, `--font-heading-style`, `--font-body-family`, `--font-body-weight`, `--font-body-style`).
- Verifica la base de `rem` antes de escribir tamaños (en Dawn, `html` usa `calc(var(--font-body-scale) * 62.5%)`: con escala 1, `1rem` ≈ 10px).
- Revisa tamaño calculado y legibilidad en móvil y escritorio.

## 7. Idioma, voz y personalidad

Consulta público, personalidad y comunicación en `context/PROJECT.md`.

- Usa el idioma y la variante regional confirmados.
- Respeta tono y expresiones aprobadas en botones, avisos, errores y textos comerciales.
- Usa las traducciones del tema para cadenas reutilizables de interfaz.
- No inventes reseñas, cifras, garantías, certificaciones, descuentos ni promesas de producto.

## 8. Principios de experiencia

- Prioriza las necesidades del público y los objetivos documentados.
- Da a cada sección una función y una jerarquía clara.
- Facilita navegación, descubrimiento, selección de variantes y compra.
- Explica condiciones comerciales cerca del punto donde ayudan a decidir.
- Diseña y revisa móvil junto con escritorio.
- No introduzcas urgencia, promociones o elementos comerciales sin fundamento real.

## 9. Rendimiento, accesibilidad y SEO

### Imágenes y recursos

- Sin carga diferida en la imagen principal que determina el LCP; prioridad alta solo para el recurso realmente prioritario.
- Carga diferida fuera del viewport inicial; imágenes responsivas con dimensiones o proporciones que eviten saltos de layout.
- CSS y JavaScript según la necesidad del componente; sin dependencias ni preloads innecesarios.

### Accesibilidad

- HTML semántico, etiquetas claras y jerarquía lógica de encabezados.
- Navegación por teclado, foco visible y manejo de foco en drawers y modals.
- Contraste verificado en las combinaciones reales del sistema visual.
- Áreas táctiles de al menos 44 × 44 px en controles principales.
- `alt` descriptivo en imágenes informativas y `alt=""` en decorativas; iconos decorativos ocultos a tecnologías de asistencia.
- Respeta preferencias de movimiento reducido.

### SEO

- Un H1 claro por página; sin H1 duplicados por secciones añadidas.
- Conserva metadatos, URLs y datos estructurados existentes; no dupliques ni añadas información no verificada.

### Capas y overlays

- Inspecciona el sistema de capas del tema antes de añadir `z-index`.
- Mantén badges y overlays locales por debajo de navegación, carrito y modals globales; contextos de apilamiento locales solo cuando sean necesarios.

## 10. Componentes Shopify

Define los componentes según el alcance de esta tienda, no según el catálogo de otra marca. Para cada necesidad, decide entre configurar el tema, adaptar una pieza existente, crear una pieza reutilizable o posponerla. Los componentes deben respetar `context/DESIGN.md` y resolver una necesidad documentada en `context/PROJECT.md`.

Consulta `context/pages/` para el orden y contenido de cada página. No reordenes secciones ni sustituyas textos definidos por el usuario sin instrucción. Una jerarquía documentada no confirma precios, condiciones o integraciones pendientes.

## 11. Experiencia de producto

- Usa atributos relevantes al tipo de producto y a las dudas del cliente.
- Mantén claros precio, variantes, disponibilidad y acción de compra.
- Preserva formulario de producto, actualización de variantes y relación con el carrito.
- No traslades atributos de otra categoría sin que apliquen al catálogo real.

## 12. Datos específicos de la tienda

Antes de consumir metacampos o metaobjetos, verifica sus definiciones y regístralos en `context/references/DATA.md`.

- No inventes namespaces, claves, tipos ni identificadores.
- Documenta cómo se comporta cada componente cuando falta el dato.
- No almacenes secretos en el registro.

## 13. Flujo de trabajo y validación

1. Lee el contexto y determina la etapa y el alcance solicitado.
2. Revisa la arquitectura y los cambios existentes antes de editar.
3. Identifica pendientes que afecten el trabajo.
4. Implementa solo el alcance autorizado, conservando cambios del usuario.
5. Verifica páginas e interacciones afectadas en móvil y escritorio.
6. Ejecuta Theme Check y las comprobaciones disponibles.
7. Comprueba compatibilidad con el editor cuando haya entorno accesible.
8. Informa qué cambió, cómo se verificó y qué no pudo comprobarse; registra decisiones nuevas en `context/DECISIONS.md`.

El storefront se trabaja en Liquid, CSS y JavaScript nativo, sin build de frontend por defecto.

Integraciones existentes a conservar: {{INTEGRACIONES}} (por ejemplo, scripts que participan en el carrito). Revisa su contrato antes de modificar ese flujo.

## 14. Operaciones externas y publicación

- La autorización se deriva de las instrucciones del usuario y del alcance vigente.
- Un documento de otro proyecto no autoriza cambios en esta tienda.
- Verifica dominio y tema de destino antes de escribir en Shopify.
- Preparar o editar localmente no autoriza publicar ni modificar productos, precios, inventario o canales.
- Si falta una decisión o autorización, prepara lo que pueda revisarse y solicita solo la información imprescindible.

## 15. Pendientes de preparación

- {{PENDIENTES}}

Consulta `README.md` para el flujo completo y `PROMPTS.md` para los prompts de cada etapa.
