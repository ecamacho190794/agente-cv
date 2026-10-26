# Workflow: aplicación a una vacante

**Identificador:** `job-application`
**Versión:** `1.0`
**Estado:** diseñado para ejecución interactiva
**Entrada principal:** descripción de vacante proporcionada por el usuario
**Fuente profesional canónica:** `knowledge/cv_final.md`
**Registro de postulaciones:** `knowledge/postulaciones.md`
**CV adaptado:** `knowledge/cv_{empresa}.md`

## 1. Objetivo

Preparar una aplicación para una vacante concreta: comprender sus requisitos, compararlos con la experiencia documentada del usuario, preguntar por brechas relevantes y producir un CV fiel, claro y adaptado.

El CV debe estar escrito en español aunque la oferta esté en otro idioma. Debe ser fácil de leer por personas y sistemas automáticos de selección, incluidos parsers y herramientas basadas en IA. Esto significa usar una estructura estándar y términos pertinentes respaldados por evidencia; no garantiza superar filtros ni obtener una entrevista.

El flujo crea o actualiza el registro `knowledge/postulaciones.md` y genera un CV específico para la empresa. Los cambios confirmados que solo pertenecen a esta candidatura se documentan allí. No se agregan por defecto al perfil canónico.

## 2. Activación

Activa este workflow cuando el usuario solicite iniciar una aplicación y proporcione el texto de la vacante.

Ejemplo:

> Inicia el flujo de aplicación a una vacante. La vacante es la siguiente:
> [descripción de la vacante]

Antes de empezar, lee íntegramente este archivo y `AGENTS.md`.

## 3. Archivos y responsabilidades

### Entrada obligatoria

- `knowledge/cv_final.md`: fuente canónica del perfil profesional.
- Descripción de la vacante pegada o proporcionada por el usuario.

Si `cv_final.md` no existe, detén el flujo e indica que primero se debe completar el perfil. No sustituyas esta fuente por `cv_inicial.md`, salvo que el usuario solicite expresamente cambiar el análisis y acepte sus limitaciones.

### Archivos que puede crear o modificar

- `knowledge/postulaciones.md`: registro acumulativo. Si existe, añade una entrada nueva sin borrar ni reescribir entradas anteriores. Si no existe, créalo.
- `knowledge/cv_{empresa}.md`: CV en español adaptado a esta vacante. El nombre de empresa se convierte en un identificador de archivo sencillo, conservando el nombre oficial dentro del contenido.
- `knowledge/cv_final.md`: actualización opcional, adicional a las dos salidas base, solo con datos nuevos confirmados y aprobación afirmativa específica del usuario. No alteres ni elimines hechos existentes. Registra la procedencia y fecha de cada adición.

No modifiques `cv_inicial.md` ni otros archivos no enumerados aquí.

### Archivos ya existentes

- No reemplaces una entrada previa en `postulaciones.md`. Si la misma vacante ya aparece y el usuario inicia de nuevo este flujo, conserva el registro anterior y crea una entrada con un nuevo ID y fecha para esta versión.
- No sobrescribas un CV existente. Si `cv_{empresa}.md` ya existe, crea `cv_{empresa}_{AAAA-MM-DD}.md`; si ese nombre también existe, agrega un sufijo secuencial (`-02`, `-03`, etc.). Registra la ruta exacta en `postulaciones.md`.
- Para el nombre de archivo, normaliza el nombre de empresa a minúsculas, elimina diacríticos, sustituye espacios por guiones y retira caracteres no seguros para nombres de archivo. Conserva el nombre oficial original dentro del CV y el registro.
- No escribas sobre `cv_final.md` hasta que el usuario haya confirmado que desea persistir la información nueva. Si no autoriza, conserva esos datos solo en la entrada de postulación.

## 4. Reglas de interacción

1. Comprueba los archivos de entrada y salida antes de escribir.
2. Pregunta por datos indispensables ausentes. El nombre de la empresa es obligatorio para nombrar y registrar el CV. Si falta, pregunta al usuario; no lo deduzcas por un dominio, logotipo o nombre de producto.
3. Identifica otros datos faltantes importantes para evaluar la vacante, como cargo, ubicación o modalidad, y pregúntalos solo si son necesarios o el usuario podría conocerlos. No inventes respuestas.
4. Pregunta de forma interactiva por las brechas de requisitos que puedan cambiar sustancialmente el CV o la evaluación. Formula una pregunta principal por turno, agrupando subpreguntas concretas solo cuando faciliten la respuesta.
5. Acepta respuestas como “no lo he usado”, “no recuerdo”, “no estoy seguro” o “prefiero dejarlo pendiente”. No insistas después de que el usuario marque un dato como desconocido o no aplicable.
6. Distingue experiencia laboral, proyectos personales, formación, familiaridad y conocimiento teórico. No los presentes como equivalentes.
7. Después de recopilar información nueva relevante, pregúntale si desea añadirla también a `cv_final.md`. La respuesta afirmativa debe ser explícita. Si responde que no o no contesta, no persistas esa información en el perfil canónico.
8. Si la respuesta es afirmativa, confirma qué afirmaciones concretas se agregarán y su nivel de detalle antes de editar el perfil. No interpretes una respuesta sobre una brecha como autorización para actualizar el perfil.
9. Cuando sea posible, muestra al usuario un resumen breve de los hallazgos y de las limitaciones antes de crear los archivos finales.

## 5. Análisis de la vacante y correspondencia

Lee toda la descripción y extrae, cuando estén presentes:

- Empresa y nombre exacto del puesto.
- Ubicación, modalidad, tipo de empleo y nivel.
- Responsabilidades principales.
- Requisitos obligatorios y deseables.
- Lenguajes, frameworks, plataformas, herramientas y dominio del negocio.
- Experiencia, formación, idiomas y certificaciones solicitados.
- Fecha límite, enlace o identificador de la vacante, solo si aparecen en la entrada.

Registra el idioma original de la descripción. Si hay varios idiomas, señala los detectados; no es necesario traducir el anuncio completo en el índice.

Clasifica cada requisito respecto al perfil como:

- **Coincidencia respaldada:** evidencia directa en `cv_final.md`.
- **Coincidencia parcial o transferible:** experiencia relacionada documentada, sin afirmar equivalencia completa.
- **Por confirmar:** posible experiencia que requiere respuesta del usuario.
- **Brecha confirmada:** el usuario indica que no tiene esa experiencia o no logra confirmarla.

Conserva referencias a las secciones o afirmaciones de `cv_final.md` que respalden las coincidencias. Las síntesis deben mantener el sentido y el grado de certeza de la evidencia.

No trates como requisito una preferencia deseable. No penalices como carencia una condición que el anuncio no exige.

### 5.1 Preguntas sobre brechas

Consulta al usuario cuando una experiencia no aparezca en `cv_final.md` y pueda cambiar materialmente la correspondencia o el contenido del CV. Pregunta qué hizo, dónde/cuándo, en qué contexto y con qué nivel de participación. Para una métrica, pregunta por el método o base de cálculo; no inventes cifras.

Las sugerencias de tecnologías son ayudas de memoria solamente. Aplícalas a cualquier lenguaje, herramienta o tecnología mencionada en la vacante. Confirma uso real antes de incluirlas como experiencia. Si el usuario confirma una habilidad, documenta su contexto de forma proporcionada y no infieras años, nivel experto, uso profesional o dominio por una mención aislada.

## 6. Ajuste y estimación

Calcula un **porcentaje orientativo de ajuste a los requisitos** para resumir la correspondencia, no una probabilidad real de contratación. Usa una tabla de requisitos con peso explícito: obligatorio = 2, deseable = 1; coincidencia respaldada = 1, parcial = 0.5, brecha o no confirmada = 0. Divide los puntos obtenidos entre los puntos posibles y redondea al entero más cercano. Si la oferta no permite distinguir categorías o no contiene requisitos suficientes, marca el porcentaje como “no calculable” y explica por qué.

No presentes el porcentaje de ajuste como “probabilidad de quedar”. El resultado de contratación depende de factores no disponibles, como el número y perfil de otros candidatos, criterios internos, entrevistas y cambios en la vacante. En `postulaciones.md`, incluye:

- **Probabilidad aproximada de contratación:** `No estimable con la información disponible`.
- **Ajuste orientativo a los requisitos:** porcentaje calculado y método resumido.

No inventes una probabilidad numérica para satisfacer la petición de precisión aparente.

## 7. Preparación del CV adaptado

Genera un CV completo, no un análisis de la vacante ni una carta de presentación. El documento debe estar en español y reflejar la experiencia real del usuario con la selección, el orden y el énfasis apropiados para este puesto.

Usa, según corresponda, una estructura legible por ATS:

1. Nombre y datos de contacto respaldados por el perfil.
2. Título profesional alineado con el puesto, sin atribuir un cargo que el usuario no haya tenido.
3. Resumen profesional conciso y específico.
4. Habilidades pertinentes que tengan respaldo y contexto suficiente.
5. Experiencia profesional en orden cronológico inverso, con cargos, empresas y fechas fieles.
6. Proyectos relevantes, diferenciados de empleo remunerado.
7. Formación, certificaciones e idiomas, con sus niveles originales.

Adapta el vocabulario al anuncio cuando el término describa fielmente una habilidad o responsabilidad documentada. Se permiten traducciones correctas y sinónimos habituales, manteniendo nombres propios y tecnologías. No añadas bloques de palabras clave ocultos, repeticiones artificiales ni términos que el usuario no respalde. No cambies fechas, títulos oficiales, nivel de dominio, métricas ni alcance de responsabilidades.

Prioriza logros y experiencias pertinentes, pero no elimines información necesaria para que la trayectoria sea comprensible. Si el perfil no acredita un requisito, no lo redactes como habilidad; puedes reflejar experiencia relacionada con sus límites claros. No incluyas brechas ni comentarios editoriales en el CV adaptado, salvo que el usuario los pida.

## 8. Registro en `postulaciones.md`

Mantén un índice legible con una entrada independiente por postulación o versión. Usa IDs con el patrón `POST-AAAAMMDD-NN`, donde la fecha es local y `NN` es un consecutivo de dos dígitos para ese día. No reutilices un ID, incluso si se reintenta la misma vacante. Cada entrada debe contener:

- ID de postulación y fecha de creación local (`AAAA-MM-DD`).
- Estado de preparación: `en preparación`, `preparación completa`, `bloqueada` o `cancelada`.
- Entregables con estados separados:
  - `CV adaptado`: `no generado`, `generado` o `validación incompleta`; incluye ruta y fecha.
  - `CV de entrega`: estados `no generado`, `generado` o `validación incompleta`; sus versiones registran ruta, fecha, formato y validación.
  - `Carta de presentación`: estados `no generada`, `generada` o `validación incompleta`; sus versiones registran ruta, fecha, idioma y validación.
  No uses el estado general ambiguo `CV generado`.
- Una nueva entrada comienza con `Estado de preparación: en preparación`; `CV adaptado` y `CV de entrega` inician como `no generado`, y `Carta de presentación` como `no generada`.
- Empresa y puesto (o `No especificado`, si no aplica; el nombre de empresa sí debe obtenerse antes de generar el CV adaptado).
- Ubicación, modalidad y enlace/identificador, solo si se conocen.
- Ruta exacta del CV adaptado.
- Idioma original de la oferta e idioma del CV (`español`).
- Resumen de la oferta y lista breve de requisitos principales.
- Palabras clave relevantes para una futura carta de presentación: guarda los términos originales de la oferta, en su idioma original, agrupados por responsabilidades, competencias, tecnologías y motivaciones del puesto cuando corresponda. Para cada grupo, señala cuáles tienen respaldo en `cv_final.md` o en respuestas confirmadas de esta postulación, cuáles son transferibles y cuáles no deben afirmarse por falta de evidencia. Estas palabras clave orientan la redacción; no se copian automáticamente como competencias del candidato.
- Coincidencias, experiencia transferible, brechas y respuestas nuevas relevantes.
- Porcentaje de ajuste calculado, o motivo por el que no pudo calcularse.
- Probabilidad aproximada de contratación: `No estimable con la información disponible`, salvo que existan datos de selección fiables proporcionados expresamente por el usuario y un método documentado.
- Nuevos datos exclusivos de esta candidatura, tanto si fueron persistidos en `cv_final.md` como si no. Para cada dato, registra su estado de confirmación, contexto, procedencia y decisión de persistencia.
- Cambios de énfasis realizados en el CV y referencias a las afirmaciones del perfil usadas.
- Limitaciones, preguntas pendientes y fecha de última actualización.

No guardes una copia completa de la descripción si un resumen fiel y los requisitos capturados permiten identificar la vacante. Puedes conservar una cita breve cuando sea necesaria para explicar un requisito ambiguo.

Durante la entrevista, puedes guardar en la entrada de postulación el estado y los datos confirmados necesarios para poder reanudarla. No marques la preparación como completa ni el CV adaptado como generado hasta que los dos archivos base estén escritos y validados. Al terminar correctamente, marca `Estado de preparación: preparación completa` y `CV adaptado: generado` con su ruta y fecha; deja `CV de entrega` y `Carta de presentación` como `no generado` hasta que sus respectivos workflows los creen.

## 9. Persistencia opcional en `cv_final.md`

Solo procede si el usuario aprobó expresamente incorporar las afirmaciones concretas.

1. Comprueba nuevamente que `cv_final.md` sigue siendo el archivo esperado y que las afirmaciones no estén ya registradas.
2. Añade cada dato en la sección y experiencia correspondientes; conserva su procedencia indicando que fue confirmado por el usuario durante la postulación, junto con la fecha y el ID de postulación.
3. No conviertas datos exclusivos de una candidatura, como interés por una empresa, motivación para ese puesto o respuestas especulativas, en hechos profesionales generales.
4. Mantén desacuerdos, aproximaciones e incertidumbres como tales. No sustituyas datos anteriores sin preguntar expresamente.
5. Vuelve a leer el archivo y valida que no se hayan perdido ni alterado datos no relacionados.
6. Registra en `postulaciones.md` qué afirmaciones se añadieron y la autorización del usuario.

Si no puedes mantener la integridad del perfil o no puedes comprobar el resultado, no lo modifiques; deja la información en la postulación e informa la limitación.

## 10. Validación y archivos existentes

Antes de declarar el flujo completo, verifica:

- El `cv_final.md` usado era la fuente canónica y fue leído.
- Las coincidencias y brechas tienen respaldo identificable.
- Las respuestas nuevas están separadas de la información previa del perfil.
- La decisión de persistencia se respetó.
- El CV está en español, completo, consistente y adaptado a requisitos respaldados.
- No contiene competencias, logros, métricas, cargos, fechas o niveles inventados.
- El CV es legible por parsers comunes (encabezados estándar, orden lineal, sin tablas complejas ni contenido oculto).
- `postulaciones.md` conserva sus entradas previas y contiene la ruta correcta del CV nuevo.
- No se sobrescribió ningún artefacto anterior.
- Si se autorizó actualizar `cv_final.md`, se verificó el archivo después de escribir.

Si falta información indispensable y el usuario no puede proporcionarla, conserva el estado como `en preparación` o `bloqueada`, según corresponda, y no marques el CV adaptado como generado.

## 11. Informe de finalización

Responde en español e indica:

1. Estado: completado, parcial o bloqueado.
2. Empresa, puesto y fecha registrados.
3. Ruta del CV creado y del registro actualizado, solo si los verificaste.
4. Resumen del ajuste, principales coincidencias y brechas.
5. Aclara que el porcentaje es de ajuste, no probabilidad de contratación; indica que esta última no puede estimarse con rigor si faltan datos de selección.
6. Indica qué información nueva se mantuvo solo en la postulación y cuál se añadió a `cv_final.md`, si corresponde.
7. Limitaciones o información pendiente.
8. Confirma que `cv_inicial.md` no fue modificado.

No reproduzcas innecesariamente datos personales en la respuesta.
