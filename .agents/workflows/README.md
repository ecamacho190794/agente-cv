
# Índice de workflows

## Workflows disponibles

### 1. Extracción inicial del CV

- **Identificador:** `extract-cv`
- **Archivo:** `extract-cv.md`
- **Objetivo:** extraer y estructurar toda la información profesional presente en el CV inicial.
- **Entrada:** archivo de CV indicado por el usuario.
- **Salida canónica:** `knowledge/cv_inicial.md`
- **Ejecución:** bajo demanda.
- **Creación:** una sola vez.
- **Modificación posterior:** prohibida desde este workflow y desde cualquier otro workflow ordinario.

### 2. Completar y enriquecer el CV

- **Identificador:** `complete-cv`
- **Archivo:** `complete-cv.md`
- **Objetivo:** descubrir y documentar mediante una entrevista interactiva los detalles de cada empleo, las competencias técnicas, los logros, el contexto y las habilidades interpersonales.
- **Entrada:** `knowledge/cv_inicial.md`.
- **Salida canónica:** `knowledge/cv_final.md`.
- **Estado de entrevista:** `knowledge/cv_completion_state.md`.
- **Ejecución:** interactiva, bajo demanda y reanudable.
- **Creación:** el perfil final se crea una sola vez durante la entrevista inicial.
- **Modificación posterior:** requiere un flujo independiente de actualización autorizado por el usuario.
- **Fuente para procesos posteriores:** `knowledge/cv_final.md`.

### 3. Aplicación a una vacante

- **Identificador:** `job-application`
- **Archivo:** `job-application.md`
- **Objetivo:** comparar una vacante con el perfil canónico, resolver brechas mediante preguntas al usuario y crear un CV adaptado con un registro de postulación.
- **Entrada:** descripción de la vacante proporcionada por el usuario y `knowledge/cv_final.md`.
- **Salidas base:** `knowledge/postulaciones.md` y `knowledge/cv_{empresa}.md` (con sufijo si el archivo ya existe).
- **Actualización opcional:** puede añadirse información confirmada a `knowledge/cv_final.md` únicamente tras autorización afirmativa del usuario; esta es una modificación adicional al perfil, no una tercera salida base.
- **Ejecución:** interactiva, bajo demanda.
- **Idioma de salida:** español; se registra también el idioma original de la vacante.

### 4. Crear una carta de presentación

- **Identificador:** `cover-letter`
- **Archivo:** `cover-letter.md`
- **Objetivo:** redactar una carta de presentación específica para una vacante registrada, usando la oferta y el CV adaptado correspondiente.
- **Activación:** `Inicia el flujo para crear una carta de presentación para mi oferta en la empresa {nombre de la empresa}.`
- **Entradas:** entrada pertinente de `knowledge/postulaciones.md` y el CV adaptado que allí se referencia.
- **Salida:** `output/carta de presentación {empresa}.md`; su ruta, fecha e idioma quedan registrados en la postulación.
- **Idioma:** idioma original de la oferta registrado en `postulaciones.md`.

### 5. Exportar el CV de una postulación

- **Identificador:** `export-application-cv`
- **Archivo:** `export-application-cv.md`
- **Objetivo:** producir el CV de entrega para una vacante concreta, optimizado para lectura humana y parsers ATS mediante información respaldada.
- **Activación:** `Inicia el flujo para exportar el CV de mi oferta en la empresa {nombre de la empresa}.`
- **Entradas:** postulación pertinente de `knowledge/postulaciones.md`, perfil `knowledge/cv_final.md` y CV adaptado asociado.
- **Salida predeterminada:** PDF en `output/`; se usa otro formato si el usuario indica un formato especial.
- **Idioma:** idioma de la oferta registrado en `postulaciones.md`.
- **Registro:** guarda en la entrada de postulación la ruta, fecha, formato y resultado de validación del documento exportado.

### 6. Actualizar el perfil canónico

- **Identificador:** `update-cv-profile`
- **Archivo:** `update-cv-profile.md`
- **Objetivo:** revisar y aplicar al perfil canónico cambios confirmados por el usuario, incluidos los propuestos en un estado de entrevista pendiente.
- **Activación:** `Inicia el flujo para actualizar mi perfil profesional`.
- **Entradas:** `knowledge/cv_final.md` y datos nuevos o una propuesta guardada en `knowledge/cv_completion_state.md`.
- **Salida:** actualización controlada de `knowledge/cv_final.md` solo después de mostrar los cambios y recibir aprobación explícita.

## Ciclo de los entregables de una postulación

Cada entrada de `postulaciones.md` conserva un estado general de preparación y estados separados para los entregables. La aplicación crea el `CV adaptado`; `cover-letter` y `export-application-cv` añaden después sus propios estados, rutas, fechas e información de validación sin cambiar el estado general ni los otros entregables.

## Convenciones para nuevos workflows

Cada workflow nuevo debe tener un archivo Markdown independiente y definir claramente sus entradas, procedimiento, permisos y resultados.

Antes de implementarlo, debe determinarse si necesita consultar el registro de extracción (`cv_inicial.md`), el perfil canónico enriquecido (`cv_final.md`) o un artefacto derivado de otro flujo.

Los resultados de análisis, evaluaciones y candidaturas deben almacenarse en documentos derivados separados.

Ningún workflow debe actualizar silenciosamente la fuente canónica. `job-application` puede añadir al perfil únicamente la información nueva que el usuario confirme y autorice expresamente durante ese flujo. `update-cv-profile` aplica otras actualizaciones solo tras una revisión explícita de los cambios propuestos por parte del usuario.
