
# AGENTS.md — Sistema local de candidaturas laborales

## 1. Propósito

Este repositorio contiene flujos de trabajo para analizar la trayectoria profesional del usuario y ayudarle a gestionar candidaturas laborales.

El sistema debe presentar la experiencia real del usuario de forma clara, relevante y verificable. Nunca debe inventar información para mejorar una candidatura.

## 2. Fuente única de la verdad

El sistema distingue dos documentos con funciones diferentes:

- `knowledge/cv_inicial.md`: registro inmutable de la extracción original del CV; referencia histórica y evidencia de origen.
- `knowledge/cv_final.md`: perfil profesional enriquecido; fuente canónica para todos los workflows posteriores.

Antes de completar el perfil, el workflow debe comprobar si `cv_final.md` existe y revisar `cv_completion_state.md` para decidir si puede continuar la entrevista o si se requiere un flujo de actualización independiente. La existencia del perfil final nunca autoriza a sobrescribirlo.

Ningún workflow ordinario puede modificar `cv_inicial.md`.

Ningún workflow puede modificar `cv_final.md` salvo que su procedimiento autorice expresamente esa operación. El workflow de entrevista inicial crea `cv_final.md` únicamente cuando no existe. Las futuras actualizaciones requieren un flujo independiente y autorización explícita.

Los datos sugeridos por el agente no son hechos confirmados. Las tecnologías, herramientas y competencias solo podrán presentarse como experiencia confirmada si existe evidencia del CV o una declaración explícita del usuario.

## 3. Reglas globales

- Ejecuta únicamente el workflow solicitado explícitamente.
- Antes de ejecutarlo, lee por completo su archivo de instrucciones.
- No inventes empresas, cargos, fechas, responsabilidades, métricas, tecnologías, certificaciones, idiomas, niveles de dominio ni logros.
- Distingue entre hechos explícitos, síntesis fieles, cálculos derivados y datos pendientes de confirmar.
- No confundas una habilidad mencionada con experiencia profesional demostrada ni con dominio experto.
- No modifiques archivos que no pertenezcan al flujo activo.
- No sobrescribas archivos existentes sin autorización explícita y sin que el workflow permita esa operación.
- Trata el CV y los datos personales como información confidencial. Este proyecto es local: conserva en sus archivos toda la información profesional necesaria para completar el perfil, incluyendo el progreso de la entrevista. No la transmitas a servicios externos ni la copies fuera del proyecto sin autorización. No almacenes credenciales ni secretos de acceso.
- No añadas palabras clave engañosas para superar filtros ATS.
- Conserva los nombres de tecnologías, cargos, certificaciones y empresas tal como aparecen en la fuente cuando su normalización sea dudosa.
- Usa Markdown UTF-8 y estructuras fáciles de leer por diferentes modelos de IA.
- No afirmes que has leído, escrito, validado o creado un archivo si no lo has comprobado en el entorno local.

## 4. Enrutamiento de workflows

Cuando el usuario solicite un flujo:

1. Identifica el workflow correspondiente en `.agents/workflows/`.
2. Lee sus instrucciones completas.
3. Comprueba sus precondiciones antes de realizar cambios.
4. Ejecuta exclusivamente los pasos autorizados.
5. Valida los resultados antes de declarar que el flujo terminó.

### Workflow: extracción inicial del CV

Activación de ejemplo:

"Inicia el flujo de extracción de datos de mi CV. El CV se encuentra en el archivo CV.pdf".

Procedimiento:

1. Lee `.agents/workflows/extract-cv.md`.
2. Utiliza la ruta del CV indicada por el usuario.
3. Comprueba que `knowledge/cv_inicial.md` todavía no exista.
4. Extrae, organiza y valida la información de la fuente.
5. Crea `knowledge/cv_inicial.md` únicamente si se cumplen todas las precondiciones.
6. Verifica el documento generado y comunica el resultado.

Si `knowledge/cv_inicial.md` ya existe, detente sin modificarlo ni crear una segunda versión.

## Workflow: completar el CV

Activación de ejemplo:

"Inicia el flujo para completar mi CV".

Procedimiento:

1. Lee `.agents/workflows/complete-cv.md`.
2. Comprueba que `knowledge/cv_inicial.md` existe.
3. Comprueba si existe `knowledge/cv_final.md`.
4. Si hay una entrevista incompleta y un estado recuperable, reanúdala; si ya existe `cv_final.md`, guarda respuestas y una propuesta de cambios solo en `knowledge/cv_completion_state.md`.
5. Si ya existe un perfil final completado, no lo sobrescribas ni lo actualices desde este workflow.
6. Si no existe, realiza la entrevista interactiva y guarda el progreso en `knowledge/cv_completion_state.md`.
7. Espera las respuestas del usuario durante todo el proceso.
8. Si `cv_final.md` no existía al iniciar, créalo y valídalo al concluir. Si ya existía, consérvalo intacto; para incorporar la propuesta guardada en el estado, ejecuta `update-cv-profile`, que debe mostrar los cambios y esperar aprobación explícita.

Los demás workflows deben utilizar `knowledge/cv_final.md` como fuente canónica, salvo que el usuario solicite expresamente analizar el CV original.

## Workflow: aplicación a una vacante

Activación de ejemplo:

"Inicia el flujo de aplicación a una vacante. La vacante es la siguiente: [descripción]".

Procedimiento:

1. Lee `.agents/workflows/job-application.md` por completo.
2. Comprueba que `knowledge/cv_final.md` exista y úsalo como fuente profesional canónica.
3. Pregunta al usuario por la información indispensable ausente, incluido el nombre de la empresa si no aparece en la vacante.
4. Compara requisitos y experiencia, y pregunta por brechas relevantes antes de redactar.
5. Crea o amplía `knowledge/postulaciones.md` y genera `knowledge/cv_{empresa}.md`, sin sobrescribir artefactos existentes. Son las dos salidas base.
6. Conserva en los artefactos de la postulación la información nueva confirmada, pero no la agregues a `cv_final.md` sin preguntar y recibir autorización afirmativa explícita.
7. Si el usuario autoriza la actualización, añade solo los datos confirmados, conserva la estructura y procedencia del perfil y verifica el cambio.
8. Escribe el CV en español y registra el idioma original de la oferta.

## Workflow: crear una carta de presentación

Activación de ejemplo:

"Inicia el flujo para crear una carta de presentación para mi oferta en la empresa [nombre de la empresa]".

Procedimiento:

1. Lee `.agents/workflows/cover-letter.md` por completo.
2. Busca la postulación indicada en `knowledge/postulaciones.md` y usa la ruta allí registrada para leer el CV adaptado.
3. Si hay más de una vacante posible para esa empresa, pregunta cuál desea usar.
4. Escribe la carta en el idioma original de la vacante registrado en la postulación.
5. Comprueba que `output/` y su README ya existan; no los crees ni modifiques desde este workflow.
6. Crea la carta sin sobrescribir versiones existentes y registra su ruta, fecha e idioma en el entregable de esa postulación.
7. Verifica el contenido y la ruta antes de informar que terminó.

## Workflow: exportar el CV de una postulación

Activación de ejemplo:

"Inicia el flujo para exportar el CV de mi oferta en la empresa [nombre de la empresa]".

Procedimiento:

1. Lee `.agents/workflows/export-application-cv.md` por completo.
2. Localiza la postulación y su CV adaptado en `knowledge/postulaciones.md`; consulta también `knowledge/cv_final.md` y las respuestas confirmadas guardadas para esa candidatura.
3. Usa el idioma original registrado en la postulación.
4. Comprueba que `output/` y su README ya existan; no los crees ni modifiques desde este workflow.
5. Genera un PDF estándar y legible por ATS, salvo que el usuario solicite un formato especial.
6. Guarda el CV sin sobrescribir versiones anteriores y registra su ruta y fecha en el entregable de esa postulación.
7. Verifica el contenido y la integridad del archivo antes de informar que terminó. No afirmes que la selección o el paso de filtros están garantizados.

## Workflow: actualizar el perfil canónico

Activación de ejemplo:

"Inicia el flujo para actualizar mi perfil profesional".

Procedimiento:

1. Lee `.agents/workflows/update-cv-profile.md` por completo.
2. Revisa `knowledge/cv_final.md` y la fuente de los cambios propuestos (por ejemplo, `knowledge/cv_completion_state.md`).
3. Presenta los cambios concretos para revisión y espera la aprobación explícita del usuario.
4. Solo después de la aprobación, actualiza `cv_final.md`, conserva la procedencia y valida el resultado.

## 5. Compatibilidad entre agentes

Codex es el entorno principal, pero el proyecto debe seguir siendo utilizable con Claude, Gemini y otros agentes capaces de leer y escribir archivos locales.

- Mantén las instrucciones de negocio en archivos Markdown compartidos.
- No dependas de herramientas exclusivas de un proveedor para definir la lógica de los workflows.
- Si un agente no descubre automáticamente un archivo, indícale expresamente que lo lea.
- No dupliques el contenido completo de los workflows en adaptadores específicos de cada agente.
- No supongas que otro agente tiene permisos de lectura, escritura u OCR: verifica sus capacidades reales.

## 6. Gestión de archivos

- Usa rutas relativas a la raíz del proyecto siempre que sea posible.
- Crea únicamente los directorios y archivos necesarios para el flujo solicitado.
- No modifiques el documento fuente.
- No presentes borradores incompletos como resultados definitivos.
- Si una operación falla, informa del problema y conserva los archivos preexistentes.
- Antes de crear un artefacto de creación única, comprueba que no exista.

## 7. Informe de finalización

Al terminar un workflow, comunica:

- Estado: completado, parcial o bloqueado.
- Fuente utilizada.
- Archivos creados y sus rutas.
- Validaciones realizadas.
- Limitaciones y datos pendientes.
- Confirmación de que no se modificaron los archivos protegidos.

No reproduzcas innecesariamente datos personales en el mensaje final.
