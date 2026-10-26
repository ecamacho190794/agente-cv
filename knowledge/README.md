
# Conocimiento persistente

## 1. `cv_inicial.md`

Contiene la extracción fiel del CV original y funciona como registro histórico de origen.

- Se crea mediante `extract-cv`.
- No debe modificarse después de su creación.
- Permite rastrear los datos originales.
- No es la fuente canónica para los workflows posteriores una vez creado `cv_final.md`.

## 2. `cv_final.md`

Contiene el perfil profesional enriquecido mediante la entrevista interactiva de `complete-cv`.

- Es la fuente canónica para los workflows posteriores.
- Incluye experiencia técnica, responsabilidades, logros, competencias, soft skills y contexto profesional.
- Distingue hechos confirmados, síntesis, estimaciones e información pendiente.
- No debe sobrescribirse ni actualizarse desde workflows ordinarios. `job-application` puede añadir información nueva confirmada solo con autorización afirmativa y explícita del usuario.

`cv_inicial.md` y `cv_final.md` tienen propósitos distintos: el primero conserva la extracción original; el segundo es la fuente canónica enriquecida.

## 3. `cv_completion_state.md`

Contiene el estado operativo de la entrevista.

- Registra el progreso por empleo y proyecto.
- Identifica preguntas contestadas y pendientes.
- Conserva las incertidumbres y las sugerencias tecnológicas que todavía no se han confirmado.
- Permite reanudar una entrevista incompleta.

Este archivo no es la fuente canónica del perfil profesional. Es un registro del proceso de entrevista.

## 4. Artefactos de postulación

- `postulaciones.md` mantiene el índice de las vacantes trabajadas, sus resúmenes, fechas, idioma original, evaluación orientativa y rutas a los CV adaptados.
- `cv_{empresa}.md` contiene una versión en español adaptada a una vacante concreta. Si ya existe un archivo para esa empresa, el workflow crea un nombre con sufijo para conservar la versión previa.
- Cada postulación registra un estado de preparación y un estado independiente para cada entregable: CV adaptado, CV de entrega y carta de presentación.
- Los datos confirmados para una postulación se conservan en sus artefactos locales y no se añaden a `cv_final.md` salvo autorización afirmativa y explícita del usuario.

El workflow de aplicación registra en cada postulación palabras clave de la oferta para una futura carta o CV, separadas según su respaldo en el perfil.

El workflow `export-application-cv` genera el CV de entrega de la postulación en `output/` y registra su ruta, fecha, formato y resultado de validación en la entrada correspondiente. El idioma se toma de la vacante; el formato predeterminado es PDF. El perfil canónico sigue siendo `cv_final.md`.

Las cartas de presentación y los CVs de entrega se registran como versiones independientes en su postulación. No se reemplazan referencias a versiones anteriores.

Si `complete-cv` se reanuda mientras ya existe `cv_final.md`, guarda las nuevas respuestas en `cv_completion_state.md` como propuesta pendiente. Para aplicar la propuesta, usa `update-cv-profile`; el agente debe mostrar los cambios y recibir aprobación explícita antes de modificar el perfil.

## Reglas generales

- No inventar información profesional.
- No inferir experiencia a partir de sugerencias del agente.
- Mantener las relaciones entre tecnologías, responsabilidades, proyectos y empleos.
- Preservar la procedencia y el grado de certeza de los datos.
- No almacenar secretos de acceso.
- Solicitar autorización antes de cualquier actualización del perfil canónico.

Las actualizaciones generales y las propuestas pendientes de entrevista se aplican mediante `update-cv-profile`, después de mostrar los cambios y recibir aprobación explícita. `job-application` conserva su autorización específica para añadir hechos confirmados de una postulación cuando el usuario lo aprueba.
