# Shopify Store Starter — cómo preparar una tienda antes de desarrollar

Kit de contexto y proceso para arrancar cualquier tienda Shopify con agentes (Claude Code, Codex, etc.). No contiene diseño ni código de ninguna marca: contiene **la estructura** para cargar marca, referencias y design system, y **los prompts** de cada etapa.

> ¿Primer proyecto con un cliente nuevo? Empieza por **[GUIA-INICIO.md](GUIA-INICIO.md)**: accesos, materiales a pedir, de dónde sacar el tema (Dawn u otro), cómo cargar el kit, tiempos y publicación.

## 0. Arranque rápido

**Con la skill (recomendado):** abre Claude Code en la carpeta de la nueva tienda (con el tema ya descargado, p. ej. `shopify theme pull`) y escribe:

> /shopify-store-kickoff

La skill copia esta plantilla sin sobrescribir nada, llena la ficha de `AGENTS.md` y te entrevista etapa por etapa.

**Manual:** copia el contenido de esta carpeta en la raíz del tema, reemplaza los `{{PLACEHOLDER}}` de `AGENTS.md` y sigue los pasos de abajo usando [PROMPTS.md](PROMPTS.md).

## 1. Organización

```text
AGENTS.md                         Reglas técnicas y de trabajo para agentes
README.md                         Este flujo
GUIA-INICIO.md                    Checklist práctico por cliente: accesos, tema, kit, tiempos, publicación
PROMPTS.md                        Prompts listos para copiar, por etapa
skills-lock.json                  Skills del proyecto (se instalan en .agents/skills/)
context/
  PROJECT.md                      Negocio, público, voz, oferta y objetivos
  DESIGN.md                       Sistema visual (design system) y comportamiento
  DECISIONS.md                    Registro fechado de decisiones
  brand/                          Logo, fuentes + licencias, manual de marca, fotos oficiales
  pages/
    README.md                     Guía y plantilla de páginas
    home.md, collection.md, product.md, cart.md, navigation.md
  references/
    REFERENCES.md                 Ficha de cada referencia analizada
    DATA.md                       Metacampos y metaobjetos verificados (opcional)
    visual/
      marca/ home/ coleccion/ producto/ carrito/
```

Cada documento es dueño de un ámbito: reglas técnicas → `AGENTS.md`; negocio → `PROJECT.md`; visual → `DESIGN.md`; patrones externos → `REFERENCES.md`; contenido por página → `pages/`; cambios de rumbo → `DECISIONS.md`.

## 2. Principios del proceso

- Registra información confirmada y su fuente.
- Marca cada dato como **Confirmado**, **Propuesta**, **Hipótesis** o **Pendiente por definir**. No inventes datos.
- Usa referencias para adaptar patrones, nunca para copiar otra tienda.
- Resuelve contradicciones entre documentos antes de implementar la parte afectada.
- Cuando una decisión cambie, añádela a `DECISIONS.md` y actualiza la sección afectada del documento dueño. No apiles "Actualización del día X" al inicio de los documentos.
- No guardes contraseñas, tokens ni credenciales.

Formato de decisión:

```text
Decisión:
Estado: Confirmado / Propuesta / Hipótesis / Pendiente
Fuente o responsable:
Fecha:
Afecta a:
```

## 3. Paso a paso

Cada paso tiene su prompt en [PROMPTS.md](PROMPTS.md).

### Paso 1 — Reunir materiales
Web y redes actuales, catálogo, precios, variantes, logo, manual de marca, fotografías, FAQs, reseñas reales y condiciones comerciales. Objetivo, fecha y restricciones.
- Archivos de marca → `context/brand/` (ver su README).
- **Resultado:** materiales organizados y lista de faltantes.

### Paso 2 — Completar PROJECT.md
Información general → concepto → público → personalidad → voz → oferta → competencia → objetivos → restricciones.

> Nuestro cliente busca ___ cuando ___. Le preocupa ___ y necesita comprobar ___ antes de comprar.
>
> Vendemos ___ para ___. El beneficio principal es ___. Nos diferencia ___, respaldado por ___.

- **Resultado:** por qué comprarían y qué debe comunicar la tienda.

### Paso 3 — Cargar y analizar referencias
1. Guarda capturas en `context/references/visual/<área>/` con nombres descriptivos: `ref-01-producto-selector-talla-mobile.png` (no `imagen-final-2.png`).
2. Si es una web, pega la URL en el chat: el agente la revisa con Playwright en escritorio y móvil.
3. Cada referencia queda como ficha en `REFERENCES.md`: qué patrón nos sirve, qué problema resuelve, cómo se adapta a la marca y qué evitar.

No basta con "me gusta": describe el patrón ("la guía de medidas se consulta junto al selector de talla"). Una captura muestra apariencia; la interacción se verifica en la página real.
- **Resultado:** pocas referencias, cada una con una razón concreta.

### Paso 4 — Definir DESIGN.md (design system)
Concepto creativo → colores con valores y usos → tipografías y jerarquía → fotografía → layout y espaciado → componentes → iconografía → responsive → movimiento → reglas obligatorias → implementación en Shopify (tokens) → validación.

Traduce atributos ("premium", "energético") a decisiones observables. Si falta branding, prepara una propuesta y márcala como tal.
- **Resultado:** sistema visual concreto y consistente entre páginas.

### Paso 5 — Ajustar AGENTS.md
Completa la ficha (marca, prefijo, tema, versión, dominio, idioma, etapa), verifica que las rutas existan, revisa integraciones del tema y pendientes. No importes permisos de otro proyecto.

### Paso 6 — Revisar el tema y definir la primera versión
Recorrido: **home → colección → producto → carrito → checkout**. Para cada necesidad: configurar, adaptar, crear o posponer. Documenta cada página en `context/pages/` con objetivo, secciones, textos, CTAs, destinos, activos y pendientes.

### Paso 7 — Listo para desarrollo
- [ ] Oferta, público y propuesta de valor definidos.
- [ ] Productos y colecciones del lanzamiento elegidos.
- [ ] Personalidad y tono definidos.
- [ ] Referencias anotadas y archivos identificados.
- [ ] Dirección visual definida.
- [ ] Materiales disponibles y faltantes registrados.
- [ ] Condiciones comerciales confirmadas.
- [ ] Navegación y estructura de páginas definidas.
- [ ] Alcance de la primera versión acordado.
- [ ] Pendientes que afectan identidad, estructura o compra resueltos.

Al cerrar esta etapa, pide explícitamente iniciar la implementación.

### Paso 8 — Implementar, revisar y lanzar
Implementa por bloques. Revisa móvil, variantes, carrito, navegación, accesibilidad y compatibilidad con el editor. Ejecuta Theme Check. Actualiza los documentos cuando cambie una decisión. Publica solo con autorización vigente.

## 4. Reglas al reutilizar

No traslades automáticamente colores, fuentes, público, catálogo, dominios, garantías, configuración ni permisos de publicación de otro proyecto. Lo único que se reutiliza es este método y las reglas técnicas de `AGENTS.md`.
