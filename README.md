# Agente local para candidaturas laborales

Este proyecto contiene instrucciones portables para que un agente compatible con archivos locales ayude a organizar el perfil profesional y preparar materiales para candidaturas. Los workflows viven en Markdown y no dependen de un proveedor de IA concreto.

El sistema presenta la experiencia real de forma clara y verificable. No inventa datos, no exagera competencias y no promete superar filtros ATS ni conseguir una contratación.

## Antes de empezar

1. Abre la carpeta del proyecto en el agente que vayas a utilizar.
2. Indícale que lea `AGENTS.md` completo antes de trabajar. Si el agente no descubre las instrucciones por sí mismo, pídele expresamente que lea ese archivo.
3. Pídele que ejecute únicamente el workflow que solicites y que lea completo el archivo correspondiente en `.agents/workflows/` antes de hacerlo.
4. Mantén el CV original, el perfil profesional y los materiales de candidatura en este entorno local. No autorices su transmisión a servicios externos sin decidirlo expresamente.

Los workflows se activan bajo demanda; no se ejecutan automáticamente. Si falta un requisito o una respuesta necesaria, el agente debe preguntarte y esperar. No debe declarar un resultado como completo hasta verificar los archivos que produjo.

## Workflows disponibles

| Objetivo | Cómo iniciarlo | Entrada necesaria y resultado |
|---|---|---|
| Extraer el CV original | `Inicia el flujo de extracción de datos de mi CV. El CV se encuentra en el archivo [ruta].` | Requiere la ruta del CV. Crea `knowledge/cv_inicial.md` una sola vez; si ya existe, se detiene sin modificarlo. |
| Completar el perfil | `Inicia el flujo para completar mi CV.` | Requiere `knowledge/cv_inicial.md`. Es una entrevista interactiva y reanudable; crea `knowledge/cv_final.md` si aún no existe. |
| Aplicar a una vacante | `Inicia el flujo de aplicación a una vacante. La vacante es la siguiente: [descripción completa]` | Requiere la descripción de la vacante y `knowledge/cv_final.md`. Si falta la empresa u otro dato indispensable, pregunta. Crea/actualiza `knowledge/postulaciones.md` y crea un `knowledge/cv_{empresa}.md` adaptado. |
| Crear una carta | `Inicia el flujo para crear una carta de presentación para mi oferta en la empresa [empresa].` | Requiere una postulación en `postulaciones.md` y su CV adaptado. Si hay varias vacantes de la empresa, pregunta cuál. Guarda la carta en `output/` en el idioma original de la oferta. |
| Exportar el CV de una postulación | `Inicia el flujo para exportar el CV de mi oferta en la empresa [empresa].` | Requiere una postulación, su CV adaptado y `cv_final.md`. Si hay varias vacantes de la empresa, pregunta cuál. Genera un PDF estándar legible por ATS, salvo que indiques otro formato. Usa el idioma original de la oferta. |
| Actualizar el perfil canónico | `Inicia el flujo para actualizar mi perfil profesional.` | Requiere `knowledge/cv_final.md` y los datos o propuesta de cambios. El agente te muestra los cambios y solo los aplica después de tu aprobación explícita. |

Las instrucciones completas, precondiciones, pasos, validaciones y reglas de cada flujo están en:

- `.agents/workflows/extract-cv.md`
- `.agents/workflows/complete-cv.md`
- `.agents/workflows/job-application.md`
- `.agents/workflows/cover-letter.md`
- `.agents/workflows/export-application-cv.md`
- `.agents/workflows/update-cv-profile.md`

El índice de workflows es `.agents/workflows/README.md`.

## Cómo se organiza la información

- `knowledge/cv_inicial.md`: extracción fiel del CV original, registro histórico inmutable.
- `knowledge/cv_final.md`: perfil profesional enriquecido y fuente canónica para los workflows posteriores.
- `knowledge/cv_completion_state.md`: progreso, respuestas y propuestas de la entrevista; no reemplaza al perfil canónico.
- `knowledge/postulaciones.md`: registro de vacantes, resumen, empresa, fecha, idioma original, palabras clave, ajuste y rutas/estados de entregables.
- `knowledge/cv_{empresa}.md`: CV en español adaptado a una vacante específica.
- `output/`: cartas y CVs de entrega. El nombre, idioma, fecha y validación de cada documento quedan registrados en la postulación correspondiente.

`knowledge/README.md` y `output/README.md` describen esos directorios. Son parte fija del proyecto: los workflows de carta y exportación requieren que `output/` y su README ya existan y no los crean ni modifican.

Cada postulación distingue su estado general de preparación y los estados de CV adaptado, CV de entrega y carta. Crear el CV adaptado no significa que el PDF de entrega o la carta ya existan.

## Fuente de verdad y aprobación

- `cv_inicial.md` conserva lo extraído de la fuente; no debe editarse desde otros workflows.
- `cv_final.md` es el perfil profesional canónico. Completar el perfil solo lo crea cuando no existe.
- Si se reanuda una entrevista cuando `cv_final.md` ya existe, las respuestas y los cambios propuestos se guardan en `cv_completion_state.md`. Para incorporarlos, inicia `update-cv-profile`, revisa la vista previa y aprueba explícitamente.
- Durante `job-application`, los datos nuevos confirmados se conservan en la candidatura. Solo pueden añadirse también a `cv_final.md` si autorizas explícitamente esa persistencia.
- El agente debe distinguir hechos confirmados, síntesis fieles, cálculos derivados y datos pendientes. Una tecnología mencionada no implica experiencia profesional ni dominio experto.

## Reglas de uso

1. Ejecutar solo el workflow pedido explícitamente y leer sus instrucciones completas.
2. Comprobar sus precondiciones y los archivos existentes antes de escribir.
3. No inventar ni inferir empresas, puestos, fechas, tareas, métricas, tecnologías, certificaciones, idiomas, niveles o logros.
4. Preguntarte por brechas relevantes o información indispensable; no presentar sugerencias como hechos.
5. No sobrescribir artefactos existentes. Crear versiones nuevas según el procedimiento del workflow.
6. No modificar documentos ajenos al workflow activo ni los archivos protegidos.
7. No usar palabras clave engañosas para ATS. El porcentaje calculado en una candidatura es de ajuste a requisitos, no una probabilidad real de contratación; esta última se registra como no estimable si faltan datos fiables.
8. Mantener datos profesionales y personales localmente; no transmitirlos a servicios externos sin autorización. Nunca almacenar credenciales o secretos.
9. Usar Markdown UTF-8 y conservar nombres originales de empresas, tecnologías, cargos y certificaciones cuando normalizarlos pueda cambiar su sentido.
10. Al finalizar, informar estado, fuentes, archivos creados, validaciones, limitaciones y datos pendientes, sin repetir innecesariamente información personal.

## Privacidad y GitHub

El repositorio remoto es público: cualquier persona puede leer los archivos versionados y su historial. El `.gitignore` excluye `knowledge/` y `output/`, salvo sus README, además de los nombres de CV local configurados. Antes de cada commit, revisa `git status` y el contenido preparado (`git diff --cached`) para confirmar que no se hayan añadido CVs, datos personales, secretos ni artefactos de candidaturas.

`.gitignore` ayuda a evitar inclusiones accidentales, pero no elimina del historial un archivo que ya se haya confirmado. Nunca subas información personal al repositorio público.

## Convenciones del proyecto

Para ver todos los workflows y sus entradas, consulta `.agents/workflows/README.md`. Las reglas generales de ejecución están en `AGENTS.md`. Para agregar un flujo, crea su instrucción independiente en `.agents/workflows/` y actualiza el índice y la documentación pertinente sin duplicar el procedimiento completo.
