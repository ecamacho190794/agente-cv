
# Workflow: completar y enriquecer el perfil profesional

**Identificador:** `complete-cv`
**Versión:** `1.0`
**Estado:** diseñado para ejecución interactiva
**Entrada principal:** `knowledge/cv_inicial.md`
**Salida canónica:** `knowledge/cv_final.md`
**Estado de entrevista:** `knowledge/cv_completion_state.md`

## 1. Objetivo

Construir, mediante una entrevista interactiva con el usuario, un perfil profesional mucho más detallado que el CV original.

El objetivo es descubrir, documentar, estructurar y validar todas las experiencias, competencias, tecnologías, responsabilidades, logros, decisiones, métodos de trabajo y habilidades que puedan resultar útiles para futuras oportunidades laborales.

No te limites a confirmar lo que ya está escrito en el CV. Investiga activamente los detalles que normalmente se omiten por falta de espacio, por considerarse rutinarios o por no parecer relevantes para una candidatura específica.

El resultado debe permitir que otros workflows preparen candidaturas, evalúen vacantes y generen material para entrevistas sin tener que repetir toda esta entrevista.

## 2. Activación

Activa este workflow cuando el usuario solicite completar o enriquecer su CV mediante una entrevista.

Ejemplo:

"Inicia el flujo para completar mi CV".

Antes de empezar, lee íntegramente este archivo y las instrucciones globales de `AGENTS.md`.

## 3. Archivos y responsabilidades

### Entrada obligatoria

`knowledge/cv_inicial.md`

Contiene la información extraída del CV original y constituye la base para iniciar la entrevista.

Si no existe, detén el flujo e indica al usuario que primero debe ejecutar `extract-cv`.

### Salida canónica

`knowledge/cv_final.md`

Contiene el perfil profesional enriquecido, consolidado y validado con las respuestas del usuario.

Es el documento que consultarán los workflows posteriores para obtener información profesional.

### Archivo de estado

`knowledge/cv_completion_state.md`

Contiene el estado de la entrevista, las preguntas pendientes, las respuestas registradas, las áreas exploradas y las dudas que aún deben resolverse.

No debe confundirse con el perfil profesional. Su propósito es permitir que la entrevista se retome sin perder el progreso.

### Regla de integridad

Nunca modifiques `knowledge/cv_inicial.md`.

Nunca sobrescribas un `knowledge/cv_final.md` existente desde una ejecución inicial de este workflow.

Si `cv_final.md` ya existe, nunca lo sobrescribas desde este workflow. Si el estado indica que la entrevista inicial está incompleta, puedes reanudarla y registrar nuevas respuestas y una propuesta de cambios en `cv_completion_state.md`, sin editar `cv_final.md`. Al terminar, indica que la propuesta no fue aplicada. Para incorporarla, el usuario debe iniciar `update-cv-profile`, revisar los cambios concretos y aprobarlos explícitamente. Si la entrevista ya está completada, no la repitas; las correcciones o adiciones también requieren `update-cv-profile`.

Si existe `cv_final.md` pero no hay un estado que permita determinar si está completo, no lo sobrescribas ni asumas que puede descartarse.

## 4. Reglas de interacción

Este workflow requiere interacción real con el usuario.

1. Formula preguntas y espera las respuestas antes de avanzar cuando la respuesta sea necesaria.
2. No simules respuestas ni completes información basándote en probabilidades.
3. No ejecutes toda la entrevista en una sola generación ni produzcas una lista interminable de preguntas sin esperar interacción.
4. Haz una pregunta principal cada vez, con subpreguntas concretas cuando ayuden a recuperar detalles.
5. Puedes ofrecer varias opciones de respuesta para facilitar el recuerdo, pero permite siempre una respuesta libre.
6. No presupongas que el usuario recuerda fechas exactas, versiones o nombres de herramientas.
7. Acepta respuestas como "no recuerdo", "no estoy seguro", "no aplica" o "prefiero dejarlo pendiente".
8. No insistas repetidamente en un dato que el usuario haya indicado que no recuerda.
9. Permite volver a una respuesta anterior si el usuario quiere corregirla.
10. Después de cada respuesta sustancial, registra la información en el estado de entrevista antes de continuar.
11. Si el entorno no permite guardar archivos durante la conversación, explica la limitación y no afirmes que el progreso quedó persistido.
12. Cuando el usuario quiera detenerse, guarda el progreso y explica cómo reanudarlo.

Agrupa las preguntas relacionadas cuando sea eficiente, pero prioriza una conversación manejable y profunda frente a un cuestionario masivo.

## 5. Filosofía de descubrimiento

La entrevista debe descubrir experiencia real, no solamente verificar el CV.

Investiga tanto:

- Información explícita del documento original.
- Información omitida que el usuario recuerda.
- Competencias implícitas en tareas que el usuario describe, siempre confirmadas antes de incorporarlas como hechos.
- Tecnologías relacionadas que puedan ayudar a activar recuerdos.
- Decisiones técnicas, problemas y resultados que el usuario no describió inicialmente.
- Habilidades interpersonales y de colaboración.
- Experiencias difíciles de clasificar que podrían ser relevantes para otras vacantes.

No presupongas que una persona ha utilizado una herramienta por haber trabajado con una tecnología relacionada.

Las sugerencias sirven para recordar, no para demostrar experiencia.

## 6. Fase inicial: revisión del CV inicial

Antes de formular preguntas:

1. Lee completamente `knowledge/cv_inicial.md`.
2. Revisa las secciones, las experiencias, los proyectos, las tecnologías y los datos pendientes de confirmar.
3. Identifica los puestos y proyectos que requieren una entrevista individual.
4. Detecta afirmaciones vagas, responsabilidades genéricas, periodos poco claros y logros sin contexto.
5. Identifica tecnologías mencionadas sin detalles sobre su uso.
6. Prepara una lista interna de temas que deben investigarse.
7. Comprueba si existe una entrevista anterior que pueda reanudarse.

Explica brevemente al usuario qué etapas tendrá la entrevista y comienza con la primera pregunta.

No muestres un inventario enorme de preguntas de una sola vez.

## 7. Fase de orden y contexto profesional

Antes de entrar en cada empleo, confirma cuando sea necesario:

- Si el orden de los empleos es correcto.
- Si existen puestos, proyectos o periodos que no aparecen en el CV.
- Si algún cargo tuvo responsabilidades diferentes a las que sugiere el título.
- Si existen periodos con varios empleos simultáneos.
- Si faltan fechas de inicio o finalización.
- Si el usuario desea aclarar el contexto general de su trayectoria.

No exijas fechas exactas cuando no puedan recordarse. Registra el grado de precisión disponible.

Después, entrevista cada puesto de manera independiente.

## 8. Fase principal: entrevista empleo por empleo

Para cada empleo, crea una ficha de investigación independiente.

No pases al siguiente puesto hasta que hayas explorado las áreas relevantes del puesto actual, hayas registrado los datos pendientes y el usuario confirme que desea continuar o dejar el resto pendiente.

### 8.1. Contexto del puesto

Investiga:

- Empresa y sector.
- Producto o servicio.
- Tipo de clientes y usuarios.
- Tamaño y composición del equipo, si se recuerda.
- Cargo oficial y responsabilidades reales.
- Fecha de inicio y fin, incluyendo incertidumbres.
- Tipo de contratación y modalidad, si resulta relevante y el usuario desea compartirlo.
- Posición del usuario dentro del equipo.
- Personas con las que colaboraba.
- Autonomía y nivel de responsabilidad.
- Cambios de cargo, equipo o alcance durante el periodo.

### 8.2. Responsabilidades reales

No te limites a repetir las responsabilidades del CV.

Pregunta qué hacía el usuario durante una semana habitual y qué tareas realizaba ocasionalmente.

Investiga, cuando corresponda:

- Desarrollo de funcionalidades.
- Mantenimiento de sistemas existentes.
- Corrección de errores.
- Diseño de soluciones.
- Revisión de código.
- Testing.
- Despliegues.
- Administración de infraestructura.
- Migraciones.
- Soporte técnico.
- Atención a clientes.
- Mentoría.
- Documentación.
- Coordinación de tareas.
- Decisiones técnicas.
- Gestión de incidentes.
- Optimización de rendimiento.
- Seguridad.
- Automatización.
- Integración de servicios.
- Participación en decisiones de producto.

Cada responsabilidad debe estar respaldada por una respuesta del usuario o por información explícita del CV.

### 8.3. Stack tecnológico completo

Investiga todas las tecnologías utilizadas en el puesto, no solo las que aparecen en el CV.

Explora las categorías pertinentes:

- Lenguajes de programación.
- Frameworks.
- Librerías.
- Paquetes y dependencias.
- Bases de datos.
- Sistemas de caché.
- Colas y procesamiento asíncrono.
- APIs e integraciones.
- Frontend.
- Infraestructura y sistemas operativos.
- Servicios cloud.
- Docker y contenedores.
- CI/CD.
- Herramientas de observabilidad.
- Seguridad y autenticación.
- Control de versiones.
- Herramientas de colaboración.
- Testing.
- Gestión de proyectos.
- Otros sistemas específicos del dominio.

Por cada tecnología relevante, pregunta según corresponda:

- ¿La utilizaste realmente en ese puesto?
- ¿Para qué la utilizabas?
- ¿En qué proyecto o funcionalidad?
- ¿Con qué frecuencia?
- ¿La utilizabas directamente o solo interactuabas con ella?
- ¿Recuerdas la versión?
- ¿Qué nivel de responsabilidad tenías?
- ¿La configurabas, desarrollabas sobre ella, la mantenías o solamente consumías sus servicios?

No preguntes todas estas cuestiones mecánicamente para cada elemento. Adapta la profundidad a la respuesta.

### 8.4. Profundización específica según la tecnología

Aplica esta exploración a cualquier lenguaje, framework, librería, base de datos, servicio cloud, plataforma, herramienta o tecnología que aparezca en el CV o que el usuario mencione. No presupongas un stack por el cargo o sector. Adapta las preguntas a la función y al contexto de cada tecnología confirmada. Por ejemplo, para un lenguaje puedes explorar versiones, paradigmas y uso; para un framework, arquitectura y componentes; para una base de datos, modelado y consultas; para infraestructura, configuración, despliegue y operación. Son ejemplos orientativos, no listas obligatorias.

Según corresponda, investiga versiones aproximadas, contexto y propósito de uso, componentes o capacidades concretas, configuración, desarrollo, integración, mantenimiento u operación, responsabilidades personales, decisiones y problemas resueltos, y relación con proyectos y otras tecnologías.

Ruby on Rails es solo un ejemplo de cómo adaptar preguntas a una tecnología confirmada. No le des tratamiento especial frente a otros stacks ni presentes sugerencias de un ecosistema que el usuario no haya mencionado.

**Ejemplo condicional: Ruby on Rails y su ecosistema**

Si Rails aparece en la experiencia confirmada, puedes explorar áreas pertinentes como Active Record, migraciones, jobs, APIs, autenticación, rendimiento y mantenimiento. Si las herramientas específicas pueden ayudar a recordar, ofrece solo unas pocas sugerencias de la categoría pertinente y confirma el uso. Aplica el mismo procedimiento, con ejemplos propios del ecosistema, a cualquier otra tecnología mencionada.

Para cada framework, paquete, librería o herramienta confirmado, investiga su propósito, uso concreto, nivel de participación y contexto del proyecto. Si el usuario no recuerda nombres exactos, acepta descripciones funcionales y registra la identificación como pendiente de confirmar.

No incorpores una tecnología a la experiencia confirmada simplemente porque el usuario reconozca su nombre. Debe confirmar que realmente la utilizó.

### 8.5. Exploración tecnológica adaptativa

No limites las preguntas a listas predefinidas, pero tampoco intentes cubrir todas las categorías de manera mecánica. Prioriza lo que tenga relación con la experiencia confirmada, el alcance del puesto y los objetivos profesionales del usuario, si los ha expresado.

Si el usuario menciona una tecnología, genera nuevas preguntas relacionadas con el contexto que acaba de describir.

Ejemplo:

Si confirma que utilizó Sidekiq, investiga qué trabajos procesaba, cómo se configuraban las colas, cómo se gestionaban los errores y reintentos, cómo se monitorizaban los trabajos y qué problemas resolvió.

Si menciona PostgreSQL, investiga consultas complejas, índices, transacciones, migraciones, rendimiento, modelado de datos y otras áreas pertinentes.

Si menciona AWS, pregunta por los servicios concretos que utilizó y por las responsabilidades que tenía sobre ellos.

Si menciona Docker, investiga cómo construía imágenes, organizaba servicios, gestionaba variables de entorno y desplegaba aplicaciones.

Las preguntas adicionales deben depender de lo que el usuario confirme. No conviertas la entrevista en una lista de tecnologías hipotéticas.

### 8.6. Arquitectura y decisiones técnicas

Investiga:

- Monolito, monolito modular, microservicios u otros enfoques.
- Límites entre componentes.
- Patrones de diseño.
- Decisiones sobre bases de datos.
- Integraciones externas.
- Estrategias de caché.
- Procesamiento síncrono y asíncrono.
- Escalabilidad.
- Seguridad.
- Observabilidad.
- Migraciones y refactorizaciones.
- Deuda técnica.
- Alternativas consideradas.
- Motivos de las decisiones.
- Consecuencias positivas y negativas.

Distingue entre decisiones tomadas por el usuario y decisiones heredadas de otros equipos.

### 8.7. Testing y calidad

Investiga:

- Tests unitarios.
- Tests de integración.
- Tests funcionales o de sistema.
- Tests de aceptación.
- Pruebas manuales.
- Estrategias de regresión.
- Dobles de prueba y mocks.
- Herramientas y frameworks.
- Organización de suites.
- CI.
- Flakiness.
- Gestión de errores.
- Code review.
- Linting y análisis estático.
- Pruebas de rendimiento.
- Seguridad.

Pregunta qué hacía personalmente el usuario y qué responsabilidades pertenecían a otras personas.

No presupongas que una herramienta de testing se utilizó por el simple hecho de aparecer en el stack.

### 8.8. Infraestructura, despliegues y operaciones

Cuando corresponda, investiga:

- Hosting y proveedores cloud.
- Servidores y sistemas operativos.
- Contenedores.
- Orquestación.
- Pipelines CI/CD.
- Entornos de desarrollo, staging y producción.
- Variables de entorno y secretos.
- Gestión de bases de datos.
- Backups y restauración.
- Logs y métricas.
- Alertas.
- Monitorización.
- Gestión de incidentes.
- Disponibilidad.
- Rendimiento.
- Rollbacks.
- Migraciones en producción.
- Seguridad operativa.

Distingue entre administrar una plataforma, contribuir a ella y simplemente desplegar código mediante herramientas existentes.

### 8.9. Problemas difíciles y resolución de incidentes

Busca ejemplos concretos de situaciones donde el usuario:

- Resolvió un bug complejo.
- Mejoró una consulta lenta.
- Redujo tiempos de respuesta.
- Corrigió problemas de concurrencia.
- Resolvió errores de producción.
- Mejoró la estabilidad.
- Migró sistemas.
- Eliminó trabajo manual.
- Integró sistemas incompatibles.
- Desbloqueó a otros equipos.
- Investigó un problema sin documentación suficiente.

Para cada caso, investiga:

1. Contexto y problema.
2. Síntomas y restricciones.
3. Cómo investigó la causa.
4. Herramientas y métodos utilizados.
5. Alternativas consideradas.
6. Solución aplicada.
7. Participación individual frente a la del equipo.
8. Resultado observado.
9. Cómo se verificó el resultado.
10. Qué aprendió.

No inventes métricas cuando no existan. Un resultado cualitativo real también es valioso.

### 8.10. Logros e impacto

Ayuda al usuario a descubrir resultados que quizá no documentó en el CV.

Investiga:

- Tiempo ahorrado.
- Reducción de errores.
- Mejoras de rendimiento.
- Reducción de trabajo manual.
- Mejora de mantenibilidad.
- Entregas más rápidas.
- Mejora de estabilidad.
- Reducción de incidencias.
- Experiencia del cliente.
- Impacto comercial.
- Capacidad de atender más usuarios o datos.
- Mejora de colaboración.
- Reducción de deuda técnica.
- Mejora de cobertura o calidad de tests.

Pregunta por evidencia disponible, cifras aproximadas y métodos de cálculo.

Si el usuario no puede cuantificar el impacto, registra el resultado cualitativo. No conviertas una estimación informal en una métrica precisa.

### 8.11. Colaboración y liderazgo

Investiga la participación del usuario en:

- Code reviews.
- Mentoría.
- Onboarding.
- Documentación.
- Discusiones de arquitectura.
- Coordinación con producto y diseño.
- Colaboración con QA, DevOps u otros equipos.
- Comunicación con clientes.
- Priorización de tareas.
- Resolución de desacuerdos.
- Delegación.
- Liderazgo técnico.
- Gestión de incidentes.
- Presentación de propuestas.

No asumas que un cargo senior implica todas estas responsabilidades.

### 8.12. Soft skills y competencias conductuales

Investiga comportamientos concretos en lugar de limitarte a preguntar qué soft skills posee el usuario.

Explora:

- Comunicación.
- Colaboración.
- Autonomía.
- Priorización.
- Resolución de problemas.
- Pensamiento crítico.
- Adaptabilidad.
- Aprendizaje autónomo.
- Mentoría.
- Liderazgo.
- Negociación.
- Gestión de conflictos.
- Gestión de expectativas.
- Comunicación de riesgos.
- Manejo de presión.
- Responsabilidad.
- Iniciativa.
- Orientación al usuario.
- Capacidad de documentación.

Para cada competencia relevante, solicita un ejemplo real cuando sea posible.

Registra el comportamiento y su contexto como evidencia. No asignes automáticamente niveles de competencia como "experto" o "excelente".

### 8.13. Información adicional

Explora también, cuando corresponda:

- Herramientas internas.
- Sistemas propietarios.
- Dominio del negocio.
- Procesos regulatorios.
- Restricciones de seguridad.
- Trabajo con datos sensibles.
- Requisitos de disponibilidad.
- Trabajo con equipos distribuidos.
- Comunicación en otros idiomas.
- Participación en contratación.
- Contribuciones de código abierto.
- Presentaciones técnicas.
- Documentación especializada.
- Trabajo interdisciplinario.
- Responsabilidades que el usuario considere demasiado pequeñas para aparecer en un CV.

No descartes detalles simplemente porque parezcan rutinarios.

## 9. Preguntas de ayuda de memoria

Cuando una respuesta sugiera que puede haber información omitida, presenta una lista corta de posibilidades relevantes para cualquier tecnología mencionada. Adapta cada lista al ecosistema correspondiente; son ayudas de memoria, nunca supuestos de experiencia.

Ejemplo de formulación adaptable:

"Has mencionado [tecnología]. ¿Qué tareas realizabas con ella y recuerdas haber usado herramientas o componentes específicos para esas tareas? Puedo sugerirte unos pocos ejemplos del ecosistema correspondiente si ayudan a recordar; también puedes decirme que no recuerdas los nombres o que no usaste otros."

Reglas:

- Introduce las opciones como ejemplos, no como afirmaciones.
- No sugieras listas enormes sin contexto.
- Adapta las opciones a las respuestas previas.
- Permite responder "ninguna", "otras", "no recuerdo" o "no estoy seguro".
- No interpretes el silencio ni la falta de recuerdo como confirmación.
- No repitas una sugerencia ya resuelta salvo que exista una razón concreta.
- No registres tecnologías sugeridas como experiencia confirmada.

## 10. Registro de respuestas y niveles de certeza

Cada dato relevante debe mantener su estado de evidencia.

Utiliza las siguientes categorías:

- `confirmado_por_usuario`: el usuario declara explícitamente que el dato es correcto.
- `respaldado_por_cv`: el dato aparece en el documento original.
- `sintesis_confirmada`: resumen de información que el usuario revisó y confirmó.
- `estimacion_del_usuario`: aproximación expresada por el usuario, no una cifra exacta.
- `pendiente_de_confirmar`: existe incertidumbre.
- `no_recuerda`: el usuario indica que no recuerda.
- `no_aplica`: el usuario confirma que el tema no corresponde.
- `sugerido_no_confirmado`: posibilidad presentada por el agente que todavía no constituye experiencia confirmada.

No conviertas estados de incertidumbre en hechos.

Si una respuesta contiene varios datos, sepáralos para facilitar su verificación y reutilización.

Si el usuario corrige una respuesta anterior, conserva como vigente la versión corregida. Registra una nota de corrección cuando la discrepancia sea importante.

## 11. Gestión de preguntas y progreso

El archivo `knowledge/cv_completion_state.md` debe permitir retomar la entrevista.

Debe contener:

- Versión del workflow.
- Estado general.
- Si `cv_final.md` existía al iniciar o si este workflow lo creó.
- Estado del perfil canónico: pendiente de creación, creado, existente sin cambios o propuesta pendiente para `update-cv-profile`.
- Fecha de última actualización.
- Empleos y proyectos identificados.
- Empleo o proyecto activo.
- Fases exploradas.
- Temas pendientes por empleo.
- Preguntas formuladas.
- Respuestas relevantes del usuario.
- Datos pendientes de confirmar.
- Propuesta de cambios al perfil, separada de los hechos ya guardados en `cv_final.md`.
- Estado de la propuesta: no aplica, pendiente de revisión, aprobada y aplicada, o rechazada.
- Tecnologías sugeridas y estado de confirmación.
- Correcciones realizadas.
- Próxima pregunta recomendada.
- Confirmación de qué contenido se ha guardado en disco.

Después de cada respuesta sustancial:

1. Interpreta la respuesta sin añadir hechos.
2. Actualiza el estado de entrevista.
3. Comprueba que la actualización se haya escrito correctamente.
4. Formula la siguiente pregunta o presenta un resumen breve para validar cuando sea necesario.

No es necesario guardar una transcripción literal completa si los datos estructurados preservan fielmente la información. Conserva citas textuales cuando la formulación exacta sea importante.

Si no puedes guardar el estado, dilo explícitamente y no prometas que la sesión podrá retomarse automáticamente.

## 12. Estructura de `cv_final.md`

El archivo final debe ser un perfil profesional estructurado, no un CV promocional ni una transcripción de la entrevista.

Debe incluir:

1. Metadatos y procedencia.
2. Resumen profesional confirmado.
3. Contacto y perfiles profesionales.
4. Trayectoria profesional completa.
5. Una ficha exhaustiva por empleo.
6. Proyectos profesionales y personales.
7. Formación académica.
8. Certificaciones y cursos.
9. Stack tecnológico y contexto de uso.
10. Inventario de gemas, paquetes, librerías y herramientas.
11. Arquitectura, patrones y decisiones técnicas.
12. Testing y calidad.
13. Infraestructura, cloud, despliegue y operaciones.
14. Problemas complejos y soluciones.
15. Logros, impacto y métricas.
16. Liderazgo, colaboración y soft skills.
17. Conocimiento de dominio.
18. Idiomas.
19. Preferencias laborales expresamente confirmadas.
20. Afirmaciones profesionales reutilizables.
21. Preguntas pendientes, incertidumbres y límites de evidencia.
22. Guía de uso para futuros workflows.

Cada empleo debe tener una ficha propia con responsabilidades, tecnologías, ejemplos concretos, logros y competencias asociadas.

Los detalles deben conservar su relación con el empleo, proyecto o contexto en que ocurrieron.

No conviertas el archivo en una lista plana de tecnologías sin contexto.

## 13. Control de calidad

Antes de finalizar:

- Comprueba que todas las experiencias del CV inicial están representadas.
- Verifica que cada empleo haya sido explorado o esté marcado explícitamente como pendiente.
- Comprueba que las respuestas no hayan sido convertidas en hechos distintos de lo que el usuario declaró.
- Comprueba que las tecnologías sugeridas no confirmadas estén claramente separadas.
- Verifica las fechas, las relaciones entre empleos y las métricas.
- Comprueba que los logros no estén exagerados.
- Comprueba que las competencias conductuales estén respaldadas por ejemplos o declaraciones del usuario.
- Comprueba que los datos sensibles no se hayan ampliado por inferencia.
- Verifica que el archivo sea legible por otras IAs.
- Vuelve a leer los archivos escritos y comprueba su integridad.

No declares la entrevista completa únicamente porque todas las preguntas iniciales hayan sido formuladas.

## 14. Criterio de finalización

El workflow puede finalizar cuando:

1. Todos los empleos y proyectos relevantes hayan sido explorados en proporción a la información disponible y a los objetivos del usuario, o el usuario haya decidido dejarlos pendientes.
2. Se hayan revisado las áreas técnicas y conductuales pertinentes para cada contexto.
3. El usuario haya tenido oportunidad de confirmar los resúmenes importantes.
4. Las incertidumbres estén registradas.
5. El usuario confirme que desea finalizar la entrevista.
6. Si `cv_final.md` no existía al iniciar la entrevista, se haya generado y validado. Si ya existía, debe permanecer intacto y la propuesta de cambios quedar guardada en `cv_completion_state.md`.
7. El estado refleje si el perfil se creó o permaneció intacto, y si hay una propuesta pendiente para `update-cv-profile`.

Si el usuario decide finalizar con áreas pendientes, guarda esas áreas como pendientes y solicita confirmación de que acepta terminar con esas limitaciones.

No inventes información para cumplir los criterios de completitud.

## 15. Informe final

Al completar el workflow, comunica:

- Estado final.
- Ruta de `knowledge/cv_final.md`, si se creó o ya existía; aclara que este workflow no lo actualiza cuando ya existe.
- Número de empleos y proyectos documentados.
- Áreas investigadas.
- Principales temas pendientes.
- Confirmación de que `cv_inicial.md` permanece intacto.
- Confirmación de que los futuros workflows deben consultar `cv_final.md`.
- Si existía una propuesta pendiente, indica que debe revisarse mediante `update-cv-profile` antes de incorporarla al perfil canónico.

No reproduzcas innecesariamente todos los datos personales en el mensaje final.
