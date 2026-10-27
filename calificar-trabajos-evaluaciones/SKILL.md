---
name: "calificar-trabajos-evaluaciones"
description: "Use when a teacher asks you to grade a scanned worksheet, quiz, exam, assignment or other written evaluation ('taller', 'trabajo', 'evaluación') for any course — builds a grading rubric, an Excel file with live formulas, and PDF result reports."
---

# Calificar trabajos y evaluaciones (plantilla pública)

Skill genérico para calificar trabajos escaneados — talleres, quices, exámenes, tareas o cualquier otra evaluación escrita — y generar una hoja de Excel con fórmulas vivas más reportes en PDF. Basado en el flujo de trabajo real de un profesor de matemáticas y geometría en Colombia — adáptalo a tu institución, tus cursos y tu rúbrica antes de usarlo.

> Antes de usarlo: reemplaza los datos de ejemplo (profesor, institución, cursos, nota mínima) por los tuyos, y ajusta la rúbrica a tu materia. Donde el texto dice "taller" o "Taller-NN", aplica igual a cualquier otro tipo de trabajo o evaluación que califiques (quiz, examen, tarea, proyecto, etc.) — solo cambia el nombre de la carpeta según corresponda.

## 0. Antes de empezar

Si llevas un documento o proyecto con el historial de rúbricas vigentes por curso, la estructura de carpetas y acuerdos recientes, léelo primero. Este skill resume el proceso general para que funcione igual aunque ese documento no exista.

## 1. Estructura de carpetas (si hay computador conectado)

```
Calificaciones/<Curso>/Taller-NN/escaneos/   <- PDF(s) escaneados (pueden llegar en varios archivos; combínalos al calificar)
Calificaciones/<Curso>/Taller-NN/resultado/  <- Excel + 2 PDFs combinados (orden de escaneo + alfabético) + individuales/
```

Si te piden calificar un taller/curso nuevo, crea esa misma estructura antes de pedir que suban los escaneos. Si el curso nuevo corresponde al mismo grupo físico que otro curso ya calificado (mismo grado/sección), compara los nombres leídos del escaneo contra el roster de ese otro curso — suele ser el mismo roster, lo que permite corregir nombres mal leídos usando la lista ya oficial en vez de adivinar.

## 2. Definir la rúbrica

1. Lee una muestra representativa (o todo) del PDF escaneado. Identifica los ejercicios reales, la clave de respuestas resuelta de forma independiente (nunca copiada de un estudiante), y los patrones de error que ya se repiten entre varios estudiantes.
2. Arma una rúbrica por puntos. Dos estilos típicos:
   - **Holística por ejercicio** (ej. 25/15/10/5/0): un solo puntaje por ejercicio.
   - **Por subcriterios** (ej. Centro 6 + Radio 4 + Gráfica/Ecuación 10 = 20): crédito parcial más fino cuando el procedimiento se separa en partes evaluables.
3. Si ninguna estructura es obviamente la única correcta, presenta 2–4 opciones de rúbrica (con ejemplo/preview) antes de calificar a todos los estudiantes. No asumas la estructura sin que el profesor elija, salvo que ya haya dado la rúbrica exacta.
4. Guarda la rúbrica como `.md` y muéstrasela al profesor antes o junto con la primera calificación.

## 3. Reglas de calificación (siempre)

- **Nunca adivines** contenido ilegible del escaneo: márcalo con **(*)** en Observaciones y explica la duda, en vez de inventar un valor.
- El crédito parcial va atado a errores de procedimiento **concretos y reales** encontrados en la muestra (error de signo, error de suma final, confundir radio con diámetro, etc.), no a una escala genérica.
- Las unidades de medida cuentan como parte del resultado cuando el ejercicio las requiere (ej. m² en áreas). Si el valor numérico está bien pero faltan las unidades, descuenta puntos del subcriterio correspondiente y documenta la norma usada en la rúbrica de ese taller.
- Si el escaneo trae páginas rotadas o mal orientadas, rótalas con Python/PIL antes de leerlas — no adivines el contenido de una imagen mal orientada.
- Si tu institución exige una nota mínima (ej. 10/100), aplícala con una fórmula de Excel (ej. `=MAX(10, SUM(rango))`), nunca escrita a mano.
- Si un estudiante llega al resultado final correcto por un camino confuso o con un paso intermedio mal escrito, califica por el resultado final declarado y documenta la rareza del método en Observaciones — no penalices una coincidencia si el número final es el correcto.
- Estudiante del roster sin escaneo identificado (no entregó) → nota mínima automática por fórmula, sin excepción ni pregunta adicional (ver sección 4, punto 3).

## 4. Cruce con la lista oficial (roster)

Cuando el profesor comparte un Excel con la lista oficial del curso:

1. Cruza cada nombre leído del escaneo contra el roster, corrigiendo apellidos/ortografía al formato oficial (la letra manuscrita se presta a confusiones frecuentes). Si una coincidencia es dudosa, dilo explícitamente en Observaciones.
2. Reordena las filas del Excel según el número del roster, no según el orden del escaneo.
3. Estudiante del roster no identificado en el escaneo → nota en blanco pero con fórmula viva, ej. `=IF(COUNT(rango)=0,<nota_minima>,SUM(rango))`. Nunca escribas esa nota a mano.
4. Estudiante marcado como retirado/desertor en el roster → celda de TOTAL **completamente vacía** (sin fórmula, sin valor), no recibe la nota mínima automática. Si un estudiante fue promovido/trasladado a otro grado y aun así entrega el taller de su curso *nuevo*, califícalo ahí con normalidad.
5. Si el roster no coincide con ningún nombre del escaneo, dilo claramente y sigue calificando solo con los nombres leídos, hasta que el profesor confirme o envíe el roster correcto.

## 5. Excel de calificaciones

- Reutiliza el estilo visual de un Excel de calificación anterior como plantilla si existe (copia estilos de celda con openpyxl, no reescribas el formato desde cero).
- **Nunca "quemes" (hardcodees) la nota total** — siempre fórmula viva de Excel sobre las celdas de subcriterios, incluyendo el piso de nota mínima si aplica.
- Oculta las columnas de subcriterios, deja visibles N°, Estudiante, Total (y oculta Observaciones también), salvo que te pidan verlas.
- Incluye una segunda hoja "Rúbrica" con el texto completo usado.
- Antes de entregar, **verifica los totales recalculando el archivo** (LibreOffice headless a xlsx + lectura con openpyxl `data_only=True`) — nunca asumas que la fórmula quedó bien escrita sin probarla.

## 6. PDF de resultados

- Genera **dos PDFs combinados**: uno en el orden del escaneo y otro en orden alfabético (mismo contenido, dos ordenamientos) — y además un **PDF individual por estudiante** en `individuales/`.
- Tamaño carta u oficio, **una sola página por estudiante** (tabla maestra compacta: ejercicio, clave, subcriterios, subtotal — no una tabla separada por ejercicio), salvo que te pidan otro tamaño/layout.
- Si usas reportlab con fuente Helvetica: el carácter Unicode "²" no renderiza (sale en blanco). Usa `<super>2</super>` en vez del carácter literal en cualquier Paragraph con unidades cuadradas o exponentes.
- Antes de entregar, renderiza el PDF a imagen (LibreOffice/`pdftoppm`) y revisa visualmente al menos una página normal y la de la observación más larga en los combinados, y al menos un individual — nunca entregues un PDF sin verlo primero.
- Si corriges nombres por el cruce con el roster, borra (o avisa que hay que borrar) los PDFs individuales viejos con el nombre anterior para no dejar duplicados.

## 7. Entrega

- Manda cada archivo al profesor y, si hay un computador conectado, guárdalo directamente en la carpeta `resultado` del taller (los individuales en `resultado/individuales/`).
- Si se pierde la conexión a mitad de una entrega, dilo explícitamente — no asumas que "ya quedó guardado" sin confirmar — y reintenta el guardado cuando vuelva la conexión.
- Si la carpeta rechaza el guardado porque el archivo está abierto en otra aplicación, dilo explícitamente (qué archivo y por qué) y ofrece reintentar en cuanto se cierre.

## Nota sobre datos de estudiantes

Los escaneos, rosters y resultados contienen datos personales de estudiantes, muchos de ellos menores de edad. Trátalos con el mismo cuidado que cualquier dato sensible: no los uses ni los compartas fuera del flujo de calificación, y sigue la política de protección de datos de tu institución y la normativa de tu país (en Colombia, Ley 1581 de 2012 de protección de datos personales).
