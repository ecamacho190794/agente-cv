# Workflow: crear una carta de presentación

**Identificador:** `cover-letter`
**Versión:** `1.0`
**Estado:** diseñado para ejecución bajo demanda
**Registro de vacantes:** `knowledge/postulaciones.md`
**Fuente del contenido profesional:** CV adaptado referenciado en la postulación
**Salida:** `output/carta de presentación {empresa}.md`

## 1. Objetivo

Crear una carta de presentación atractiva, concreta y específica para una vacante ya trabajada mediante `job-application`. Usa el resumen de la oferta, las palabras clave registradas y el CV adaptado correspondiente. La carta debe estar en el idioma original de la oferta, aunque el CV adaptado esté en español.

La carta debe destacar la relación entre las necesidades del puesto y la experiencia real del usuario. No promete superar filtros ni inventa motivación, competencias o logros.

## 2. Activación

Activa este workflow cuando el usuario solicite crear una carta para una empresa cuya oferta esté registrada.

Ejemplo:

> Inicia el flujo para crear una carta de presentación para mi oferta en la empresa Acme.

Antes de comenzar, lee íntegramente este archivo y `AGENTS.md`.

## 3. Entradas y precondiciones

### Entradas obligatorias

- Empresa indicada por el usuario.
- Una entrada de esa empresa en `knowledge/postulaciones.md`.
- El CV adaptado referenciado por dicha entrada.
- El idioma original de la oferta registrado en la entrada.

Si falta `postulaciones.md`, la postulación no existe o la ruta del CV no está registrada, detén el flujo e indica que primero se debe completar `job-application` para esa vacante. La carpeta `output/` y `output/README.md` forman parte fija del proyecto; si falta cualquiera, detente e informa que la estructura del proyecto está incompleta.

Si hay varias postulaciones de la empresa y no se puede determinar cuál quiso decir el usuario, pregunta cuál desea usar (por ejemplo, puesto o fecha). No elijas por intuición.

Si falta el idioma original o está marcado como incierto, pregunta al usuario antes de redactar. No infieras el idioma a partir del nombre de la empresa.

Lee por completo la entrada pertinente de `postulaciones.md` y el CV adaptado asociado. No uses `cv_final.md` ni `cv_inicial.md` como sustituto del CV indicado, y no busques la oferta en internet.

## 4. Archivos y permisos

### Archivos que puede leer

- `knowledge/postulaciones.md`
- El CV adaptado cuya ruta consta en la postulación.

### Archivos que puede crear o modificar

- La carta de presentación en `output/`.
- Solo los campos del entregable “Carta de presentación” en la entrada correspondiente de `knowledge/postulaciones.md`: ruta, fecha, idioma y estado de validación.

No modifiques el CV adaptado, `cv_final.md`, `cv_inicial.md`, `output/README.md` ni otras entradas de `postulaciones.md`.

### Nombre y colisiones

Usa el nombre oficial de la empresa, conservando espacios y acentos. Retira únicamente caracteres no permitidos o peligrosos para un nombre de archivo. El texto dentro de la carta debe conservar el nombre oficial exacto.

Si la ruta de salida ya existe, no la sobrescribas. Añade un sufijo con la fecha local (` (AAAA-MM-DD)`) antes de `.md`; si también existe, usa un contador secuencial (` (AAAA-MM-DD-02)`, etc.).

## 5. Uso de la información y palabras clave

Usa la oferta resumida, requisitos y palabras clave guardadas en `postulaciones.md` para entender qué busca la empresa. Usa el CV adaptado para conocer qué afirmaciones profesionales pueden incluirse. Conserva las etiquetas de respaldo que el workflow de aplicación guardó:

- Las palabras clave respaldadas pueden aparecer en la carta cuando ayuden a describir experiencia real.
- La experiencia transferible debe presentarse como relacionada, sin afirmar equivalencia exacta.
- Las palabras clave sin respaldo sirven para entender la vacante, pero no se presentan como habilidades del usuario.

La carta no debe añadir hechos que no estén en el CV adaptado o en datos confirmados de la postulación. No conviertas responsabilidades del empleador en logros del usuario. No inventes motivación personal, años de experiencia, impacto, liderazgo, seniority, nivel de idioma, disponibilidad, salario ni autorización laboral.

Si la postulación contiene una motivación expresada por el usuario, puedes usarla fielmente. Si una motivación personal es necesaria para una carta personalizada pero no consta, formula una pregunta breve y espera la respuesta. Si el usuario no desea añadirla, continúa con una carta basada en el puesto y la experiencia documentada, sin afirmar sentimientos o motivos no declarados.

## 6. Redacción

Redacta la carta íntegramente en el idioma original registrado en `postulaciones.md`. Mantén nombres propios y tecnologías tal como aparecen en el CV o la vacante cuando la traducción pueda generar ambigüedad.

Salvo que la postulación señale otro formato o extensión, prepara una carta de aproximadamente 200–350 palabras que:

1. Incluya saludo profesional. Usa el nombre de una persona de contacto solo si está registrado; de lo contrario, utiliza un saludo general apropiado al idioma.
2. Nombre la vacante y exprese interés únicamente de manera que no atribuya al usuario una motivación específica no confirmada.
3. Relacione dos o tres necesidades centrales del puesto con evidencia concreta del CV adaptado.
4. Incluya palabras clave de forma natural y solo como parte de afirmaciones respaldadas.
5. Cierre con una invitación profesional a conversar, sin afirmar disponibilidad u otras condiciones desconocidas.
6. Termine con el nombre del usuario solo si aparece en el CV adaptado.

Evita una carta genérica, repetir el CV en forma de párrafo, afirmaciones grandilocuentes, listas de palabras clave o contenido dirigido a manipular filtros ATS/IA. Prioriza claridad, voz natural y correspondencia demostrable.

## 7. Estructura del archivo

Guarda el resultado como Markdown sencillo:

```markdown
# Carta de presentación — {Empresa}

**ID de postulación:** {POST-AAAAMMDD-NN}
**Puesto:** {nombre del puesto}
**Fecha:** {AAAA-MM-DD}
**Idioma de la oferta:** {idioma original}
**CV relacionado:** `{ruta relativa al CV adaptado}`

{carta completa en el idioma original}
```

No incluyas notas internas, porcentajes de ajuste, brechas confidenciales ni explicaciones sobre el proceso en el cuerpo de la carta.

## 8. Registro de la carta

En la entrada identificada por su ID, registra bajo el entregable **Carta de presentación** cada versión con ruta exacta, fecha local de creación, idioma y resultado de validación. Marca la versión `generada` solo después de validarla; si la validación queda incompleta, regístrala como `validación incompleta`. Si ya existe una versión anterior, conserva su historial y agrega la nueva versión. No cambies el estado general de la postulación ni el estado de los otros entregables.

## 9. Validación

Antes de declarar el flujo completo, verifica:

- Se utilizó la entrada correcta de la empresa, vacante y CV.
- La carta está en el idioma original registrado.
- Las afirmaciones sobre el usuario tienen respaldo en el CV adaptado o en información confirmada de la postulación.
- Las palabras clave aparecen naturalmente y no convierten requisitos sin respaldo en habilidades.
- El nombre del puesto, empresa, fecha y ruta del CV son correctos.
- No se sobrescribieron archivos.
- El archivo de carta se volvió a leer y está íntegro.
- `output/README.md` ya existía y no fue modificado.

Si faltan entradas o evidencia esenciales, informa la limitación y no presentes un borrador como carta final.

## 10. Informe de finalización

Responde en español e indica:

1. Estado: completado, parcial o bloqueado.
2. Empresa, vacante e idioma utilizados.
3. Ruta exacta de la carta, solo si se verificó.
4. Fuente utilizada: registro de postulación y ruta del CV adaptado.
5. Limitaciones, si las hubo.

No reproduzcas datos personales innecesariamente.
