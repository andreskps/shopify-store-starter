# Guía de inicio — cualquier tema, cualquier cliente

Checklist práctico para arrancar un proyecto Shopify nuevo con este kit, de cero a "listo para desarrollar". El método detallado está en [README.md](README.md) y los prompts en [PROMPTS.md](PROMPTS.md).

---

## 0. Requisitos (una sola vez por equipo)

| Herramienta | Para qué | Comprobar |
|---|---|---|
| Node.js LTS | Shopify CLI, `npx skills`, Playwright | `node -v` |
| Shopify CLI | Descargar, previsualizar y subir temas | `shopify version` |
| Git | Historial y respaldo del tema | `git --version` |
| Claude Code (u otro agente) | Ejecutar la skill y los prompts | `claude --version` |
| Skill global `shopify-store-kickoff` | Automatiza el arranque | Escribe `/shopify-store-kickoff` en Claude Code |

---

## 1. Con el cliente, antes de tocar código

### Acceso a la tienda
- Pide **acceso de colaborador** (Partner Dashboard → Tiendas → Agregar tienda → código de solicitud de colaborador) o una cuenta de staff con permiso de **Temas**.
- Confirma el dominio `xxxx.myshopify.com`.
- Nunca pidas ni guardes contraseñas en el repositorio.

### Materiales que debe enviar el cliente
Envíale esta lista tal cual:

- [ ] Logo (SVG o PNG transparente), variantes claro/oscuro
- [ ] Manual de marca o guía de estilo, si existe
- [ ] Fuentes (archivos + licencia web) o nombre de las que usan
- [ ] Fotografía de producto y lifestyle aprobada
- [ ] Catálogo: productos, variantes, precios, colecciones
- [ ] Condiciones comerciales: envíos, devoluciones, pagos, promociones reales
- [ ] Preguntas frecuentes y reseñas reales (con permiso de uso)
- [ ] Web y redes actuales, competidores y 3–5 tiendas que les gusten (con el *porqué*)
- [ ] Objetivo del proyecto, fecha de lanzamiento y restricciones (apps, presupuesto, legales)

Lo que no llegue se registra como **Pendiente por definir**; no bloquea el arranque.

---

## 2. Crear la carpeta del proyecto

Una carpeta por cliente, con nombre corto de la marca:

```bash
mkdir -p ~/Desktop/NOMBRE-MARCA && cd ~/Desktop/NOMBRE-MARCA
```

---

## 3. Elegir de dónde sale el tema

| Caso | Comando | Notas |
|---|---|---|
| **A. Tema que el cliente ya tiene** (gratis o de pago) | `shopify theme pull --store xxxx.myshopify.com` y elige el tema | Trabaja sobre un **duplicado**, nunca sobre el live. Duplica primero desde Admin → Tienda online → Temas. |
| **B. Empezar desde Dawn** | `shopify theme init NOMBRE --clone-url https://github.com/Shopify/dawn.git --latest` | Base que usa el kit por defecto. |
| **C. Otro tema gratuito de Shopify** (Horizon, etc.) | Instálalo en la tienda desde la Theme Store, duplícalo y haz `pull` como en A | Verifica variables y estructura (ver §7). |
| **D. Tema base de Shopify (Skeleton)** | `shopify theme init NOMBRE` | Mínimo; implica construir más componentes. |

Luego inicia git y haz el primer commit **antes** de cualquier cambio, para tener el tema original como punto de partida:

```bash
git init && git add -A && git commit -m "Tema base original"
```

Comprueba qué tema y versión es:

```bash
grep -m2 -E '"theme_(name|version)"' config/settings_schema.json
```

---

## 4. Cargar el kit

**Opción recomendada:** abre Claude Code en la carpeta y escribe:

> /shopify-store-kickoff

**Opción manual:**

```bash
cp -rn ~/Desktop/shopify-store-starter/. .
```

Después reemplaza los `{{PLACEHOLDER}}` de `AGENTS.md` y `context/` (marca, prefijo, mercado, tema, versión, dominio, idioma). `cp -rn` no sobrescribe archivos que ya existan.

### Elegir el prefijo
2–4 letras minúsculas derivadas de la marca (p. ej. `ac-` para "Acme"). Todo archivo y clase propia lo lleva: `sections/ac-hero.liquid`, `.ac-hero__title`. Confírmalo con el cliente o contigo mismo y no lo cambies después.

---

## 5. Dónde va cada cosa

| Tengo… | Va en… |
|---|---|
| Logo, fuentes, manual, fotos oficiales | `context/brand/` |
| Info del negocio, público, voz, oferta | `context/PROJECT.md` |
| Captura de una tienda que inspira | `context/references/visual/<área>/` + ficha en `REFERENCES.md` |
| URL de una tienda que inspira | Pégala en el chat → el agente la revisa y crea la ficha |
| Colores, tipografía, componentes | `context/DESIGN.md` |
| Orden y textos de una página | `context/pages/<página>.md` |
| Metacampos / metaobjetos verificados | `context/references/DATA.md` |
| "Cambiamos de idea sobre X" | `context/DECISIONS.md` |

---

## 6. Orden de trabajo y tiempos orientativos

| # | Etapa | Prompt | Entregable | Tiempo |
|---|---|---|---|---|
| 1 | Intake de materiales | PROMPTS §1 | `brand/README.md` con activos y faltantes | 0,5 día |
| 2 | Negocio y voz | §2 | `PROJECT.md` | 0,5–1 día |
| 3 | Referencias | §3a–3c | `REFERENCES.md` + capturas | 0,5–1 día |
| 4 | Design system | §4 | `DESIGN.md` | 1 día |
| 5 | Ajustar reglas | §5 | `AGENTS.md` sin placeholders | 1 h |
| 6 | Alcance y páginas | §6a–6b | `pages/*.md` | 1 día |
| 7 | Revisión de preparación | §7 | Checklist del README en verde | 1 h |
| 8 | Implementación | §8 | Tema | según alcance |

**Validación con el cliente:** al terminar las etapas 2, 4 y 6, envía el documento al cliente y registra su aprobación en `DECISIONS.md`.

---

## 7. Si el tema no es Dawn

`AGENTS.md` usa ejemplos de Dawn. Al trabajar con otro tema, revisa y ajusta:

- **Variables tipográficas y de color:** busca en `layout/theme.liquid` o en el CSS base cómo se llaman (`--font-heading-family` en Dawn; puede variar).
- **Base de `rem`:** comprueba el `font-size` de `html`.
- **Carpeta `blocks/`** (temas con theme blocks, como Horizon): el patrón de bloques reutilizables cambia.
- **Carrito y drawers:** identifica qué JS controla el carrito antes de modificarlo y anótalo en `{{INTEGRACIONES}}`.
- **Temas de pago:** respeta su licencia; documenta qué archivos del núcleo se modifican, porque las actualizaciones del proveedor pueden pisarlos.

Registra estas diferencias en la sección 3 (Arquitectura) de `AGENTS.md`.

---

## 8. Desarrollar y previsualizar sin riesgo

```bash
shopify theme dev --store xxxx.myshopify.com
```

Crea un tema de desarrollo temporal con URL de preview y editor. Para compartir una versión con el cliente:

```bash
shopify theme push --unpublished
```

Antes de cada entrega:

```bash
shopify theme check
```

Y revisa móvil (320 y 390 px) y escritorio con Playwright.

---

## 9. Publicar y entregar

- [ ] El cliente aprobó la preview del tema no publicado.
- [ ] Theme Check sin errores.
- [ ] Recorrido home → colección → producto → carrito → checkout probado.
- [ ] Copia de seguridad del tema live actual (duplicado en Admin).
- [ ] Publicación hecha **por el cliente** o con su autorización por escrito.
- [ ] `AGENTS.md` actualizado (etapa, versión de personalización) y commit con tag de versión.

---

## Reglas que no cambian entre clientes

1. Nunca traslades datos, colores, fuentes, dominios ni permisos de otro cliente.
2. No inventes reseñas, cifras, garantías ni descuentos.
3. Todo lo que el cliente quiera cambiar habitualmente debe poder cambiarse desde el editor.
4. Nunca trabajes sobre el tema live.
5. Lo que no se pudo verificar se dice explícitamente.
