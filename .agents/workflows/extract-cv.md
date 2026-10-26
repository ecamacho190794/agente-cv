
# Workflow: extracción inicial del CV

**Identificador:** `extract-cv`
**Versión:** `1.0`
**Estado:** diseñado para la primera ejecución
**Tipo:** extracción inicial, ejecutada bajo demanda
**Salida canónica:** `knowledge/cv_inicial.md`

## 1. Objetivo

Transformar el CV indicado por el usuario en un registro de extracción completo, fiel, estructurado y reutilizable por distintas IAs.

El documento debe concentrar los datos profesionales disponibles en el CV para que futuros workflows puedan consultarlos sin tener que reinterpretar el PDF original.

Este workflow extrae y organiza información. No evalúa ofertas laborales, no adapta el CV a una vacante y no inventa datos para mejorar una candidatura.

## 2. Activación

Activa este workflow cuando el usuario solicite expresamente la extracción inicial del CV.

Ejemplo:

"Inicia el flujo de extracción de datos de mi CV. El CV se encuentra en el archivo CV.pdf".

El nombre y la ruta del archivo pueden variar. Utiliza la ruta indicada por el usuario.

No inicies este workflow simplemente porque encuentres un PDF en el repositorio.

## 3. Entradas y precondiciones

### Entrada obligatoria

- Un archivo de CV accesible, normalmente en formato PDF.
- La ruta del archivo indicada por el usuario.

### Directorio de trabajo

La raíz del proyecto que contiene `AGENTS.md`.

### Archivo de salida

`knowledge/cv_inicial.md`

### Comprobaciones previas

Antes de comenzar:

1. Identifica la raíz del proyecto.
2. Confirma la ruta exacta del CV.
3. Comprueba que el archivo fuente existe y puede leerse.
4. Comprueba si `knowledge/cv_inicial.md` ya existe.

Si el archivo fuente no existe o no puede leerse, detén el flujo y solicita una ruta válida o una alternativa accesible.

Si `knowledge/cv_inicial.md` ya existe, detente sin modificarlo. Informa al usuario de que el registro de extracción ya existe y que se requiere autorización explícita para un proceso independiente de revisión o corrección.

No crees nombres alternativos como `cv_inicial_v2.md`, `cv_inicial_final.md` o `cv_inicial_nuevo.md` para eludir esta regla.

## 4. Procedimiento de extracción

### Fase A: lectura completa de la fuente

1. Determina el número total de páginas del documento.
2. Extrae el texto de todas las páginas.
3. Mantén la relación entre empresas, cargos, fechas, responsabilidades y logros.
4. Revisa encabezados, pies de página, tablas, columnas y enlaces.
5. Si el PDF contiene páginas escaneadas, utiliza OCR cuando esté disponible.
6. Registra si se utilizó texto digital, OCR o una combinación de ambos.
7. Documenta páginas ilegibles, texto cortado o cualquier limitación de extracción.

No asumas que el orden del texto extraído es correcto si el documento tiene varias columnas o tablas.

No declares que todas las páginas fueron procesadas si no puedes comprobarlo.

### Fase B: extracción de información

Extrae toda la información profesional que aparezca en el CV, incluyendo:

- Datos de contacto y perfiles profesionales.
- Titular y resumen profesional.
- Experiencia laboral.
- Cambios de cargo dentro de una misma empresa.
- Responsabilidades y logros.
- Métricas y resultados cuantificados.
- Proyectos profesionales, personales, académicos y de código abierto.
- Formación académica.
- Certificaciones y cursos.
- Lenguajes de programación y frameworks.
- Bases de datos.
- Infraestructura, nube, despliegue y DevOps.
- Testing y calidad.
- Arquitectura y prácticas de ingeniería.
- Herramientas y plataformas.
- Metodologías.
- Idiomas y niveles declarados.
- Premios, publicaciones y reconocimientos.
- Preferencias laborales expresamente declaradas.
- Otros datos profesionales relevantes.

No descartes información por considerarla poco importante para futuras ofertas. La selección y priorización de información se realizará en otros workflows.

### Fase C: normalización controlada

Puedes mejorar el formato sin alterar el significado.

- Corrige espacios, saltos de línea y errores de extracción evidentes.
- Conserva los nombres de empresas, instituciones, puestos, tecnologías y certificaciones.
- No traduzcas nombres propios ni títulos técnicos cuando la traducción pueda cambiar su significado.
- Conserva la precisión original de las fechas.
- No conviertas un año en una fecha exacta si el CV no proporciona ese detalle.
- No combines puestos distintos en una sola entrada.
- No atribuyas una tecnología a una experiencia laboral si no existe evidencia que la relacione con ella.

Si una normalización es dudosa, conserva el texto original y registra la ambigüedad.

### Fase D: verificación de evidencia

Realiza una segunda pasada comparando el contenido estructurado con el documento original.

Verifica especialmente:

- Nombres de empresas e instituciones.
- Cargos y progresión profesional.
- Fechas de inicio y finalización.
- Responsabilidades de cada puesto.
- Métricas, porcentajes y cantidades.
- Tecnologías asociadas a cada experiencia.
- Títulos académicos y certificaciones.
- Niveles de idioma.
- Enlaces y datos de contacto.
- Orden de las experiencias laborales.

Si encuentras contradicciones, registra las distintas versiones. No decidas cuál es correcta por intuición.

Cuando sea posible, anota la página o sección de origen de los datos importantes.

### Fase E: preparación del registro de extracción

1. Organiza la información según el esquema de salida definido en este archivo.
2. Utiliza etiquetas consistentes y encabezados claros.
3. Mantén separados los hechos explícitos, las síntesis fieles y los cálculos derivados.
4. Marca los datos desconocidos como `No especificado en el CV`.
5. Marca los datos ilegibles como `No legible en la fuente`.
6. Marca las incertidumbres como `Por confirmar`.
7. Incluye las limitaciones de extracción en los metadatos.
8. Crea el directorio `knowledge/` si no existe.
9. Comprueba una vez más que `knowledge/cv_inicial.md` no exista antes de escribirlo.
10. Crea el archivo canónico.
11. Vuelve a leer el archivo escrito y valida su integridad.

No presentes un documento incompleto como si fuera una extracción completa.

Si ocurre un error de escritura, no sobrescribas archivos preexistentes ni crees copias alternativas. Informa del estado real de la operación.

## 5. Reglas estrictas de veracidad

Nunca inventes:

- Empresas, cargos o fechas.
- Responsabilidades o resultados.
- Porcentajes, métricas o ahorros.
- Tecnologías utilizadas en un puesto.
- Certificaciones o estudios.
- Idiomas o niveles de dominio.
- Años de experiencia no demostrados.
- Habilidades que no aparezcan en la fuente.

No conviertas una responsabilidad en un logro cuantificado.

No interpretes la simple mención de una tecnología como prueba de dominio experto o experiencia profesional.

No infieras atributos personales a partir del nombre, la fotografía u otros indicios.

No deduzcas salario deseado, disponibilidad, autorización laboral, modalidad preferida ni disposición a reubicarse.

No visites enlaces ni afirmes haber validado su contenido si no lo has hecho realmente. Conserva la URL tal como aparece en el documento.

No añadas palabras clave con el único objetivo de manipular sistemas ATS.

Distingue siempre entre:

- **Explícito:** aparece directamente en la fuente.
- **Síntesis fiel:** resume información de la fuente sin añadir afirmaciones.
- **Cálculo derivado:** resultado calculado a partir de datos explícitos, con su base documentada.
- **Pendiente de confirmar:** información ambigua, incompleta o contradictoria.

Los cálculos derivados no deben presentarse como texto original del CV.

## 6. Estructura obligatoria del registro de extracción

El resultado debe ser un archivo Markdown UTF-8.

Utiliza los siguientes metadatos al comienzo, sustituyendo los valores de ejemplo por información real:

---
document_type: canonical_cv_profile
schema_version: "1.0"
creation_status: initial_extraction
source_file: "ruta indicada por el usuario"
source_page_count: 0
pages_processed: 0
extraction_method: "digital_text"
created_on: "AAAA-MM-DD"
---

Los valores `0` y `AAAA-MM-DD` son marcadores de ejemplo, no valores que deban conservarse. Registra los valores reales. Si un dato no puede determinarse, utiliza `unknown` cuando corresponda y explica la limitación.

Después de los metadatos, utiliza las siguientes secciones, en este orden.

# CV inicial — Registro de extracción

## 1. Metadatos y cobertura de la fuente

Incluye la ruta del archivo, número total de páginas, páginas procesadas, método de lectura y limitaciones.

## 2. Perfil profesional de la fuente

Incluye el titular profesional y el resumen original.

Si ayuda a comprender el contenido, añade una síntesis fiel claramente identificada como tal.

No reemplaces el texto original por una versión promocional.

## 3. Contacto y perfiles profesionales

Registra únicamente los datos presentes en el CV: correo, teléfono, ubicación declarada, LinkedIn, GitHub, portafolio, sitio web y otros perfiles.

## 4. Experiencia laboral

Crea una entrada independiente por cada puesto.

Para cada entrada utiliza:

- Empresa:
- Cargo exacto en la fuente:
- Ubicación:
- Fecha de inicio:
- Fecha de finalización:
- ¿La fuente indica que es el puesto actual?:
- Modalidad o tipo de empleo:
- Responsabilidades explícitas:
- Logros explícitos:
- Métricas y resultados cuantificados:
- Tecnologías, herramientas y métodos asociados al puesto:
- Equipos, clientes, productos o áreas mencionados:
- Fuente (página o sección):
- Ambigüedades o datos por confirmar:

Si hay varios cargos en una misma empresa, registra cada cargo por separado.

## 5. Proyectos

Crea una entrada por proyecto con estos campos:

- Nombre:
- Tipo o contexto:
- Propósito o problema:
- Rol:
- Fechas:
- Descripción explícita:
- Responsabilidades:
- Tecnologías:
- Resultados o métricas:
- Enlace:
- Fuente:
- Ambigüedades o datos por confirmar:

Distingue los proyectos personales de la experiencia laboral cuando la fuente permita hacerlo.

## 6. Formación académica

Para cada elemento registra:

- Institución.
- Título o programa exacto.
- Ubicación.
- Fechas.
- Estado declarado.
- Detalles adicionales.
- Fuente.

No supongas que un programa fue completado si la fuente no lo indica.

## 7. Certificaciones, cursos y formación complementaria

Para cada elemento registra:

- Nombre exacto.
- Entidad emisora.
- Fecha.
- Vigencia, si aparece.
- Identificador o enlace.
- Fuente.

No conviertas cursos en certificaciones oficiales si el CV no los identifica como tales.

## 8. Habilidades y conocimientos

Organiza las habilidades que aparecen en el CV en categorías útiles:

- Lenguajes y frameworks.
- Bases de datos y almacenamiento.
- Nube, infraestructura, despliegue y DevOps.
- Testing y calidad.
- Arquitectura y prácticas de ingeniería.
- Herramientas y plataformas.
- Metodologías y procesos.
- Otras competencias.

Para cada habilidad, registra su contexto de uso solo si está especificado.

Si una tecnología aparece en una lista general sin contexto, indícalo. No asignes niveles de dominio.

## 9. Idiomas

Para cada idioma registra:

- Nombre.
- Nivel exacto indicado.
- Certificación o evidencia declarada.
- Fuente.

No infieras niveles a partir de la nacionalidad, los estudios o el idioma en el que está escrito el CV.

## 10. Logros, premios, publicaciones y reconocimientos

Conserva las afirmaciones cuantificadas y los reconocimientos junto con su contexto y fuente.

Si un logro ya está documentado en una experiencia laboral, puedes referenciar esa entrada para evitar duplicaciones innecesarias.

## 11. Preferencias y condiciones laborales explícitas

Incluye únicamente información que el CV declare expresamente:

- Ubicación deseada.
- Modalidad.
- Disponibilidad.
- Autorización laboral.
- Tipo de empleo.
- Expectativa salarial.
- Otras condiciones declaradas.

Si no aparece información, indica `No especificado en el CV`. No infieras ni solicites esos datos durante este flujo.

## 12. Otros datos profesionales relevantes

Incluye información profesional de la fuente que no encaje de forma natural en las secciones anteriores.

## 13. Discrepancias, ambigüedades y datos por confirmar

Para cada caso registra:

- Campo afectado.
- Versiones o lecturas encontradas.
- Fuente o página.
- Motivo de incertidumbre.
- Estado: pendiente de confirmar.

Si no hay discrepancias detectadas, indícalo expresamente.

## 14. Inventario de afirmaciones reutilizables

Crea una lista de afirmaciones profesionales que otros workflows puedan reutilizar.

Cada afirmación debe tener:

- ID estable: `CLAIM-001`, `CLAIM-002`, etc.
- Afirmación factual.
- Evidencia o texto fuente.
- Fuente (página o sección).
- Tipo: explícita, síntesis fiel o cálculo derivado.
- Respaldo: alto, limitado o pendiente de confirmar.
- Límites de interpretación.

Utiliza el respaldo alto únicamente cuando exista evidencia legible y directa.

El respaldo limitado indica que la información existe, pero su contexto es parcial.

Las afirmaciones pendientes de confirmar no deben presentarse como hechos verificados.

Los IDs deben ser estables dentro del documento para facilitar referencias desde otros artefactos.

## 15. Guía para futuras IAs

Incluye este principio:

"Este archivo es el registro inmutable de los datos profesionales extraídos del CV inicial. `knowledge/cv_final.md`, cuando exista, es la fuente canónica para los workflows posteriores. No inventes, completes por intuición ni exageres afirmaciones. Comprueba el respaldo y los límites de cada afirmación antes de reutilizarla. La mención de una habilidad no demuestra nivel experto ni experiencia profesional. Si una vacante exige información ausente, registra la brecha o pregunta al usuario. No modifiques este documento desde otros workflows: crea documentos derivados separados y conserva las afirmaciones utilizadas con sus IDs y fuentes. Si detectas un error, solicita autorización para un flujo de corrección independiente."

## 7. Compatibilidad entre agentes

El documento debe ser legible por Codex, Claude, Gemini y otros agentes que puedan acceder a los archivos locales.

- Usa Markdown estándar y UTF-8.
- Mantén encabezados y etiquetas estables.
- Evita formatos dependientes de un proveedor.
- No dependas de recuerdos de conversaciones anteriores.
- Los workflows futuros deben consultar este archivo directamente.
- Los documentos derivados no pueden modificar este registro ni el perfil canónico.

## 8. Lista de validación obligatoria

Antes de declarar el flujo completado, verifica:

- [ ] El CV fuente correcto fue leído.
- [ ] El número total de páginas y las páginas procesadas están registrados.
- [ ] Todas las páginas fueron revisadas o se documentaron las limitaciones.
- [ ] Cada experiencia laboral y cambio de cargo está separado correctamente.
- [ ] Fechas, empresas, cargos, tecnologías, enlaces y métricas coinciden con la fuente.
- [ ] No se atribuyeron tecnologías o logros a puestos sin evidencia.
- [ ] Los datos desconocidos, ilegibles y contradictorios están etiquetados.
- [ ] Las 15 secciones están presentes.
- [ ] Las afirmaciones reutilizables tienen evidencia y fuente.
- [ ] El archivo se volvió a leer después de escribirse.
- [ ] El documento canónico no existía antes de esta ejecución.
- [ ] El CV original y los demás archivos permanecen intactos.

Si falla una comprobación crítica, informa un estado `parcial` o `bloqueado`, no `completado`.

## 9. Informe de finalización

Responde en el idioma del usuario e incluye:

1. Estado: completado, parcial o bloqueado.
2. Fuente: ruta del CV y cobertura de páginas.
3. Salida: ruta exacta del archivo, solo si se creó y verificó.
4. Limitaciones: páginas ilegibles, OCR dudoso, contradicciones o datos pendientes.
5. Integridad: confirma que el CV original y los demás archivos no fueron modificados.

No reproduzcas todos los datos personales en la respuesta final. Resume el resultado y señala el archivo local.
