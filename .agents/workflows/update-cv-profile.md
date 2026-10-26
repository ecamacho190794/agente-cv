# Workflow: actualizar el perfil canónico

**Identificador:** `update-cv-profile`
**Versión:** `1.0`
**Estado:** diseñado para ejecución interactiva y con aprobación explícita
**Perfil que puede actualizarse:** `knowledge/cv_final.md`
**Fuentes posibles:** usuario, `knowledge/cv_completion_state.md` u otro archivo local indicado por el usuario

## 1. Objetivo

Revisar datos profesionales nuevos o correcciones propuestos para el perfil canónico y, solo después de mostrar al usuario el cambio concreto y recibir su aprobación explícita, incorporarlos a `knowledge/cv_final.md`.

Este workflow cubre la propuesta pendiente que puede quedar después de reanudar `complete-cv` cuando el perfil ya existía, además de otras correcciones o adiciones expresamente solicitadas por el usuario. No autoriza cambios automáticos ni modificaciones a `cv_inicial.md`.

## 2. Activación

Activa este workflow cuando el usuario pida actualizar, corregir o incorporar información al perfil canónico.

Ejemplo:

> Inicia el flujo para actualizar mi perfil profesional.

Antes de comenzar, lee íntegramente este archivo y `AGENTS.md`.

## 3. Entradas y precondiciones

### Entrada obligatoria

- `knowledge/cv_final.md` existente.
- La corrección o información nueva indicada por el usuario, o una fuente local específica indicada por él.

Puede consultarse `knowledge/cv_completion_state.md` si el usuario quiere incorporar la propuesta pendiente de `complete-cv`. No infieras que el usuario quiere aplicarla solo porque exista.

Si `cv_final.md` no existe, detente: el perfil debe crearse primero mediante `complete-cv`.

## 4. Archivos y permisos

### Archivos que puede leer

- `knowledge/cv_final.md`.
- La fuente de los cambios propuestos, como `knowledge/cv_completion_state.md` o un archivo indicado por el usuario.

### Archivos que puede modificar

- `knowledge/cv_final.md`, únicamente tras la aprobación explícita descrita en la sección 5.
- `knowledge/cv_completion_state.md`, únicamente para marcar una propuesta de entrevista como aplicada o rechazada, si ese archivo fue la fuente de la actualización.

No modifiques `cv_inicial.md`, `postulaciones.md` ni otros archivos.

## 5. Revisión y autorización

1. Lee el perfil y la fuente completa.
2. Separa las afirmaciones confirmadas, las síntesis, estimaciones, dudas y datos pendientes.
3. Compara cada propuesta con `cv_final.md` para detectar duplicados, discrepancias o información que no debería pasar a un perfil general (por ejemplo, interés por una empresa específica).
4. Prepara una vista previa clara, indicando qué sección cambiará, qué texto se añadirá o corregirá, la procedencia y el nivel de certeza.
5. Pregunta al usuario si aprueba exactamente esos cambios. Espera la respuesta. Una solicitud general de “actualizar el perfil” no sustituye esta aprobación después de mostrar la propuesta.
6. Si el usuario rechaza, no modifiques `cv_final.md`; si procede, marca la propuesta de estado como rechazada.
7. Si el usuario aprueba, aplica solo los cambios mostrados. No incorpores otros datos de la fuente ni reformules hechos no incluidos en la vista previa.

Los datos locales de una candidatura solo se incorporan al perfil canónico si describen experiencia profesional general confirmada. Excluye preferencias específicas para una empresa, motivaciones de una candidatura, especulaciones y requisitos copiados de la vacante.

## 6. Procedimiento de actualización

Después de recibir aprobación explícita:

1. Verifica que `cv_final.md` no haya cambiado desde la revisión. Si cambió, vuelve a comparar y presenta una vista previa nueva para aprobación.
2. Inserta los datos en la sección y ficha de empleo/proyecto que corresponda. Conserva la relación entre la información y su contexto.
3. Añade procedencia y fecha de confirmación cuando sea útil. Mantén las categorías de evidencia y la precisión original; no conviertas estimaciones en cifras exactas.
4. No elimines ni reemplaces datos existentes salvo que la vista previa aprobada describa esa corrección de forma explícita.
5. Vuelve a leer el archivo completo o las secciones afectadas junto con sus datos relacionados. Comprueba que no haya pérdida, duplicación o alteración accidental.
6. Si el cambio provino de `cv_completion_state.md`, marca allí la propuesta como aplicada, con fecha y referencia a las secciones actualizadas. No elimines el historial de respuestas.

Si no puedes escribir o verificar la actualización, conserva los archivos previos e informa el estado real.

## 7. Validación

Antes de declarar el flujo completo, verifica:

- El usuario aprobó el texto exacto aplicado.
- Cada afirmación añadida tiene una fuente identificable y un nivel de certeza correcto.
- El cambio corresponde a experiencia o información profesional general.
- No se modificó `cv_inicial.md` ni ningún archivo fuera de los autorizados.
- El perfil actualizado se volvió a leer y permanece íntegro.
- Si la propuesta procedía del estado de entrevista, su estado de aplicación quedó actualizado sin borrar respuestas.

## 8. Informe de finalización

Responde en español e indica:

1. Estado: completado, parcial o bloqueado.
2. Secciones modificadas, sin reproducir innecesariamente datos personales.
3. Fuente de los cambios.
4. Confirmación de que el cambio exacto recibió aprobación explícita y `cv_final.md` fue validado después de la edición, solo si ocurrió.
5. Confirmación de que `cv_inicial.md` permaneció intacto.

Si el usuario no aprobó los cambios, informa que el perfil quedó sin modificar.
