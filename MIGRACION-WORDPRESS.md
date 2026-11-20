# Paso a WordPress: guía para la migración

Este prototipo (HTML estático en GitHub Pages) es la referencia visual y de contenido. La web final será WordPress, editable por la escuela, primero en un subdominio de pruebas y después en sprintidiomes.com. La idea es **no copiar el HTML tal cual**: hay que reconstruirlo limpio a partir de esta guía y de `DESIGN.md`.

## 1. Estado del prototipo (noviembre de 2026)

| Página | Estado |
|---|---|
| `index.html` (Home) | Revisada y aprobada |
| `qui-som.html` | Revisada |
| `kids-planet.html`, `kids.html`, `teens.html` | Con los cambios de Paula |
| `cambridge.html` | Con los cambios de Paula; quedan dudas pendientes de respuesta |
| `adults.html`, `frances.html`, `business.html`, `particular.html` | Pendientes de rehacer con la misma estructura |
| `cursos.html` | Sin revisar: datos antiguos (p. ej. «Màx. 10»). Decidir con Paula si se mantiene |
| `avis-legal.html`, `privacitat.html`, `cookies.html` | Faltan los datos reales (`[RAÓ SOCIAL]`, etc.) |

Limpieza hecha el 19/11/2026: eliminado el CSS que no se usaba y las declaraciones repetidas que se pisaban entre sí. Verificado con capturas píxel a píxel a 375, 768 y 1440 px (sin cambios visuales).

## 2. Base del tema

- **`theme.json`** a partir de `DESIGN.md`: colores (uno por curso), tipografías (Bricolage Grotesque, Nunito, Caveat) y la escala de tamaños (H1 76/44, H2 48/28, H3 22–24, texto 16–18).
- **Fuentes alojadas en local** (ya lo están en `fonts/`). No cargarlas desde Google.
- **Una sola hoja de estilos** del tema con los componentes de abajo. Ahora cada página lleva su CSS dentro: en WordPress no se debe repetir.
- **Menú, pie, barra de cursos y botón flotante de WhatsApp**: hoy los genera `nav.js`. En WordPress pasan a ser partes de plantilla (`header.html`, `footer.html`) y el menú se gestiona desde Apariencia → Menús. La barra de cursos coloca la pestaña activa a la vista en móvil.

## 3. Componentes (bloques o patrones reutilizables)

Las páginas de curso comparten estructura; cambia el color y el contenido.

| Componente | Dónde se usa | Qué debe poder editar la escuela |
|---|---|---|
| Portada de curso (foto, etiqueta, H1, subtítulo, 4 datos, botones) | Todas las de curso | Foto, textos, los 4 datos, enlaces de los botones |
| Etiqueta de sección + título + entradilla | Todas | Textos |
| Metodología en tarjetas | Kids Planet, Kids, Teens, Cambridge | Número de tarjetas, icono, título, texto |
| Carrusel de fotos («Un cop d'ull a les nostres classes») | Kids Planet, Kids, Teens, Cambridge | Fotos y texto alternativo. Con botón de pausa |
| Niveles | Cada curso tiene su versión: camino del conejo (Kids), escalera con bola (Teens), certificados con sello (Cambridge) | Nombre, nivel MCER y texto de cada nivel |
| Prueba de nivel (caja con botón y pregunta de ejemplo) | Teens (y Cambridge cuando Paula pase el enlace) | Textos y enlace de la prueba |
| Convocatorias (año con los meses de examen marcados) | Cambridge | Qué meses tienen examen |
| Horarios (texto a la izquierda, tabla a la derecha) | Todas las de curso | La tabla: una fila por nivel, columnas «dl+dc», «dt+dj», «dv» |
| Bàner final (conejo «Us esperem!», texto, 2 botones) | Todas las de curso | Textos y color. Misma estructura en todas |
| Formulario de contacto | Home | Debe enviar de verdad (ver punto 4) |
| Plano «Com arribar» (se amplía al pulsarlo) | Home | Imagen del plano |

Las animaciones (conejo, escalera, sellos, recorrido del método, calendario, carruseles) son scripts pequeños: cada uno con su bloque, cargado solo en la página que lo usa, y respetando «reducir movimiento».

## 4. Cosas a resolver en la migración

1. **Formulario**: hoy no envía nada. Con un plugin (Fluent Forms, Contact Form 7…), aviso de privacidad, casilla de aceptación y protección contra spam.
2. **Pruebas de nivel**: la escuela quiere saber quién las hace (con registro). Decidir si se migran tal cual o se rehacen (propuesta enviada aparte a Paula).
3. **Horarios editables** sin tocar código (campo repetible o bloque de tabla).
4. **Textos legales** con los datos reales y banner de cookies si se añade analítica.
5. **Imágenes**: ya están en WebP con versión de 700 px para móvil; mantener `srcset`.
6. **Redirecciones** de las URLs antiguas del WordPress actual a las nuevas.

## 5. Antes de publicar

Seguir la lista de `DESIGN.md` (tipografía, espacios, responsive y accesibilidad) en cada página, y además:
- Sin scroll lateral de 320 a 1920 px.
- Revisión de accesibilidad (axe, WCAG 2.2 AA) y navegación con teclado.
- Compresión gzip o Brotli activa en el hosting.
- Fuentes en local, sin grabación de sesiones ni mapas de calor sin consentimiento.
