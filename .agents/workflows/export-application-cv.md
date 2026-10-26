# Workflow: exportar el CV de una postulación

**Identificador:** `export-application-cv`
**Versión:** `1.0`
**Estado:** diseñado para ejecución bajo demanda
**Registro de vacantes:** `knowledge/postulaciones.md`
**Perfil profesional canónico:** `knowledge/cv_final.md`
**CV adaptado de referencia:** ruta registrada en la postulación
**Salida predeterminada:** PDF en `output/`

## 1. Objetivo

Exportar el CV para entregar en una postulación concreta, reuniendo la información relevante y confirmada del perfil canónico, de la entrada de postulación y del CV adaptado asociado. `knowledge/cv_final.md` sigue siendo el perfil canónico enriquecido; el archivo que crea este workflow es el CV de entrega para una vacante.

El documento debe estar en el idioma de la oferta registrado en `postulaciones.md`, tener una estructura estándar y facilitar la lectura humana y la extracción por parsers ATS. La selección de contenido debe ser fiel a la trayectoria y relevante para el puesto.

No es posible garantizar que un empleador seleccione al candidato ni que un sistema ATS acepte un documento. El workflow debe maximizar claridad, relevancia y compatibilidad técnica sin inventar datos ni manipular sistemas de selección.

## 2. Activación

Activa este workflow cuando el usuario solicite exportar el CV de entrega para una postulación registrada.

Ejemplo:

> Inicia el flujo para exportar el CV de mi oferta en la empresa Acme.

Antes de empezar, lee íntegramente este archivo y `AGENTS.md`.

## 3. Entradas obligatorias

- Nombre de la empresa indicado por el usuario.
- Entrada correspondiente en `knowledge/postulaciones.md`.
- `knowledge/cv_final.md`.
- CV adaptado referenciado por la postulación.
- Idioma original de la vacante registrado en la postulación.

Usa la entrada de postulación para seleccionar la oferta y recuperar sus palabras clave, requisitos, brechas, respuestas nuevas confirmadas, idioma y decisiones de persistencia. Usa `cv_final.md` como fuente canónica general. Lee el CV adaptado completo para conservar el enfoque ya aprobado para esa oferta.

Si hay varias vacantes para la empresa y no puede saberse cuál quiso decir el usuario, pregúntale cuál usar. Si falta una entrada, el CV adaptado o el idioma, detén el flujo e indica qué dato debe completar mediante `job-application`. No infieras el idioma ni uses el CV inicial como sustituto de `cv_final.md`. La carpeta `output/` y su README forman parte fija del proyecto; si falta cualquiera, detente e informa que la estructura del proyecto está incompleta.

## 4. Archivos y permisos

### Archivos que puede leer

- `knowledge/postulaciones.md`.
- `knowledge/cv_final.md`.
- El CV adaptado referenciado en la entrada correspondiente.
- Un archivo de formato o plantilla indicado expresamente por el usuario.

### Archivos que puede crear o modificar

- CV de entrega en `output/`.
- La entrada correspondiente en `knowledge/postulaciones.md`, únicamente para registrar el entregable “CV de entrega”: ruta, fecha, formato y resultado de validación. No reescribas otros datos de la postulación.

No modifiques `cv_inicial.md`, `cv_final.md`, el CV adaptado ni los datos de otra postulación.

## 5. Selección del formato

Por defecto, genera un archivo PDF con texto seleccionable y legible; no rasterices las páginas como imágenes.

Si el usuario especifica un formato especial para este CV (por ejemplo, HTML, XML, DOCX u otro), usa ese formato en vez del PDF, siempre que el entorno pueda producirlo y validarlo. Si el usuario menciona que tiene una plantilla o archivo de referencia pero no lo proporciona o no está accesible, pregúntale por la ruta o detén el flujo hasta obtenerlo. No sustituyas silenciosamente el formato solicitado por otro.

Si no es posible crear el formato pedido en el entorno, informa de la limitación. No afirmes que generaste el archivo. Puedes proponer un formato alternativo, pero espera la aceptación del usuario antes de cambiar el resultado solicitado.

## 6. Reconciliación de la información

Combina la información relevante de estas fuentes, manteniendo su procedencia:

1. `cv_final.md`: hechos profesionales canónicos.
2. Datos específicos y confirmados de la postulación: respuestas que se hayan quedado locales para esa vacante y no se hayan añadido al perfil.
3. CV adaptado: selección y énfasis ya preparados para esa oferta.
4. Requisitos y palabras clave de la oferta almacenados en la postulación.

No conviertas palabras clave de la empresa en competencias del candidato. Solo utiliza una palabra clave como afirmación profesional si tiene respaldo en el perfil canónico o en una respuesta explícita y confirmada para esta candidatura. Distingue coincidencias completas de experiencia transferible.

Si las fuentes discrepan, no resuelvas la contradicción por intuición. Usa la versión confirmada más específica para esta postulación únicamente si su procedencia y estado de confirmación están claros; en otro caso pregunta al usuario o deja fuera la afirmación dudosa y registra la limitación en `postulaciones.md`.

“Usar toda la información disponible” significa considerar todas las fuentes permitidas y los datos relevantes, no incluir cada detalle indiscriminadamente. Prioriza lo pertinente al puesto y conserva una trayectoria comprensible. No agregues datos nuevos en esta fase ni modifiques `cv_final.md`.

## 7. Idioma y contenido

Redacta todo el CV en el idioma original registrado para la vacante. Conserva sin cambios los nombres oficiales de empresas, cargos, instituciones, tecnologías y certificaciones cuando una traducción pudiera alterar su significado. Traduce las descripciones con fidelidad.

Incluye las secciones pertinentes, en orden claro:

1. Nombre y datos de contacto respaldados por el perfil.
2. Título profesional fiel a la trayectoria y alineado con el puesto.
3. Resumen profesional específico.
4. Competencias pertinentes con respaldo.
5. Experiencia laboral en orden cronológico inverso, con empresas, cargos y fechas fieles.
6. Proyectos relevantes claramente diferenciados del empleo.
7. Formación académica.
8. Certificaciones, cursos e idiomas, con estados y niveles tal como están documentados.

Omitir una sección vacía está permitido. No inventes logros, métricas, responsabilidades, títulos, fechas, seniority, niveles de dominio, certificaciones, disponibilidad ni autorización laboral. No transformes una habilidad mencionada en dominio experto o experiencia profesional demostrada.

## 8. Formato estándar legible por ATS

Si el usuario no indica una plantilla especial, usa un diseño profesional sobrio:

- Una sola columna y orden de lectura lineal.
- Texto real seleccionable, fuentes comunes y buen contraste.
- Encabezados descriptivos estándar, como “Experience/Experiencia”, “Skills/Competencias” y “Education/Formación”, en el idioma de la vacante.
- Fechas, puestos y empresas en una secuencia consistente.
- Viñetas simples para responsabilidades y logros.
- Diseño sin tablas complejas, columnas, cuadros flotantes, iconos, gráficos, fotografías, barras de nivel, encabezados/pies con información esencial ni texto oculto.
- Términos del anuncio incorporados de forma natural solo cuando estén respaldados.

La prioridad es que el documento pueda leerse sin diseño visual y que el texto extraído conserve el orden y los encabezados. No añadas bloques de palabras clave, repeticiones artificiales ni instrucciones dirigidas al sistema ATS.

## 9. Nombre de archivo y colisiones

Genera por defecto `output/CV de entrega {empresa} - {puesto} - {ID de postulación}.pdf`. Conserva espacios y acentos, elimina caracteres peligrosos para nombres de archivo y usa un identificador breve de puesto cuando sea necesario. Para un formato especial, conserva el mismo nombre base y usa la extensión correspondiente. El ID distingue varias postulaciones de la misma empresa.

Si el archivo ya existe, no lo sobrescribas. Añade un sufijo de fecha local (` (AAAA-MM-DD)`) antes de la extensión; si también existe, añade un contador (` (AAAA-MM-DD-02)`, etc.).

La carpeta `output/` y su README son parte del proyecto y deben existir antes de ejecutar el workflow. Si falta uno, detente e informa que la estructura del proyecto está incompleta. Este workflow no crea ni actualiza ese README.

## 10. Validación del documento

### Para cualquier formato

- Comprueba que el contenido esté en el idioma de la oferta.
- Verifica empresa, puesto, fechas, nombres propios y rutas.
- Compara cada afirmación profesional con las fuentes permitidas.
- Confirma que se consideraron los datos locales confirmados de la candidatura y que no se presentaron como persistidos en el perfil canónico.
- Revisa que no haya datos contradictorios, errores de codificación o secciones truncadas.
- Vuelve a leer el documento final.

### Para PDF

- Comprueba que el archivo se abre y contiene texto seleccionable.
- Extrae el texto del PDF y verifica el orden de lectura, encabezados, fechas y viñetas.
- Renderiza las páginas y revisa que no haya cortes, desbordamientos, páginas en blanco, texto diminuto ni elementos superpuestos, si el entorno cuenta con capacidad de inspección visual.
- Si no puedes verificar visualmente una parte, dilo en el informe y no afirmes una validación visual completa.

### Para formato especial

- Valida que el archivo sea sintácticamente correcto y abra en un lector apropiado cuando sea posible.
- Comprueba que su contenido y estructura reflejen la plantilla solicitada.
- Explica limitaciones de compatibilidad con ATS si el formato o diseño pedido pudiera dificultar la extracción.

Actualiza únicamente el registro del entregable “CV de entrega” en la postulación: añade la versión con su ruta, fecha de generación, formato y resultado de validación. Márcala `generado` solo después de validarla; si la validación queda incompleta, usa `validación incompleta`. Conserva versiones previas y no cambies el estado general de la candidatura ni los datos restantes.

Si no puedes validar un archivo o el contenido tiene problemas, no lo marques como final. Conserva el archivo preexistente y reporta el estado real.

## 11. Informe de finalización

Responde en español e indica:

1. Estado: completado, parcial o bloqueado.
2. Empresa, puesto e idioma del CV.
3. Ruta y formato del documento creado, solo si existen y fueron comprobados.
4. Fuentes utilizadas.
5. Validaciones completadas y limitaciones.
6. Confirma que `cv_final.md` y `cv_inicial.md` no fueron modificados.
7. Aclara que el formato se optimizó para legibilidad y extracción por ATS, pero no puede garantizar selección ni superar filtros particulares.

No reproduzcas innecesariamente datos personales en el mensaje.
