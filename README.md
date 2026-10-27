# Skill de Claude: Calificar trabajos y evaluaciones escaneadas

Skill para Claude (Claude Code, Cowork o la app de Claude, según lo que tu cuenta permita) que automatiza la calificación de trabajos escaneados — talleres, quices, exámenes, tareas o cualquier otra evaluación escrita: construye una rúbrica, genera un Excel con fórmulas vivas (nunca notas "quemadas" a mano) y produce reportes en PDF listos para entregar — dos combinados (por orden de escaneo y alfabético) y uno individual por estudiante.

Creado originalmente por **Alirio Rojas Villamizar** ("Profe Alirio"), profesor de Matemáticas y Geometría en Bucaramanga, Colombia, para su propio flujo de calificación, y publicado aquí como plantilla genérica para que cualquier docente lo use y lo ajuste a su contexto.

## Qué hace

- Define una rúbrica de calificación (holística o por subcriterios) a partir de una muestra de los trabajos escaneados, y la valida contigo antes de calificar a todo el curso.
- Cruza los nombres leídos del escaneo contra la lista oficial del curso (roster) y corrige errores de lectura.
- Genera un Excel con fórmulas vivas (incluida una nota mínima, si tu institución la exige) y una segunda hoja con la rúbrica usada.
- Genera PDFs de resultados: dos combinados (orden de escaneo y alfabético) y uno individual por estudiante.
- Verifica los totales recalculando el archivo y revisa visualmente los PDF antes de entregarlos.

## Qué NO incluye esta versión pública

La versión original de este skill también enviaba la nota por WhatsApp automáticamente a cada estudiante, usando automatización de navegador sobre el WhatsApp Web del profesor. Se dejó fuera de esta versión pública a propósito: depende de una configuración particular (Claude in Chrome conectado al WhatsApp Web de cada profesor) y, sobre todo, porque enviar calificaciones de menores de edad por un canal automatizado es una decisión que cada docente debe tomar con sus propias reglas de consentimiento y verificación — no algo que convenga activar por defecto en una plantilla pública. Si te interesa esa parte, puedes construirla tú mismo sobre esta base.

## Cómo usarlo

1. Descarga la carpeta `calificar-trabajos-evaluaciones/` de este repositorio (contiene `SKILL.md`).
2. Agrégala a tus skills de Claude:
   - **Claude Code**: copia la carpeta dentro de `.claude/skills/` de tu proyecto o de tu cuenta.
   - **Claude / Cowork**: si tu organización tiene habilitada la carga de skills, súbela desde la configuración de skills (como archivo `SKILL.md` o carpeta comprimida `.skill`).
3. Abre `SKILL.md` y reemplaza los datos de ejemplo (curso, institución, nota mínima) por los tuyos — está escrito para que lo ajustes, no para usarlo tal cual.
4. Pídele a Claude que califique un trabajo o evaluación escaneada, **adjuntando los PDF escaneados** en el chat (o dejándolos en la carpeta `escaneos/` si tienes tu computador conectado a Claude — ver sección 1 del skill). El skill se activa automáticamente cuando la petición coincide con su descripción; sin los escaneos no tiene nada que calificar.
5. Si quieres que cruce nombres con tu lista oficial del curso, adjunta también ese Excel (el roster) — es opcional, pero evita errores de lectura en los nombres.

## Requisitos

- Una cuenta de Claude con soporte para skills personalizados.
- Para los pasos de Excel/PDF: `openpyxl`, `reportlab`, y LibreOffice o `pdftoppm` disponibles en el entorno donde corre Claude (esto ya viene listo en Claude Code y Cowork; en otros entornos puede variar).

## Privacidad

Los trabajos, rosters y resultados contienen datos personales de estudiantes, muchos de ellos menores de edad. Antes de usar este skill con datos reales, confirma que cumples con la política de protección de datos de tu institución y con la normativa de tu país.

## Licencia

MIT — úsalo, adáptalo y compártelo libremente. Ver [LICENSE](LICENSE).
