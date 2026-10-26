
# Directorio de agentes

## Propósito

Este directorio contiene las instrucciones específicas de los workflows del sistema de candidaturas laborales.

## Estructura

- `workflows/`: procedimientos ejecutables bajo demanda.
- `workflows/README.md`: índice de workflows disponibles y convenciones para crear otros.
- `workflows/extract-cv.md`: procedimiento de extracción inicial del CV.
- `workflows/complete-cv.md`: entrevista interactiva para enriquecer el perfil.
- `workflows/job-application.md`: aplicación a una vacante y creación de un CV adaptado.
- `workflows/cover-letter.md`: carta de presentación basada en una postulación registrada y su CV adaptado.
- `workflows/export-application-cv.md`: exportación del CV de entrega para una vacante en PDF o en el formato especial indicado por el usuario.
- `workflows/update-cv-profile.md`: actualización revisada y autorizada del perfil canónico.

## Convenciones

Cada workflow debe documentar:

1. Nombre, identificador y objetivo.
2. Frase de activación.
3. Entradas requeridas y opcionales.
4. Archivos que puede leer.
5. Archivos que puede crear o modificar.
6. Precondiciones y permisos.
7. Procedimiento paso a paso.
8. Reglas de veracidad y privacidad.
9. Formato de salida.
10. Validaciones de calidad.
11. Comportamiento ante errores o archivos existentes.
12. Informe de finalización.

## Compatibilidad

La carpeta `.agents/` es una convención interna del proyecto; no todos los agentes la detectarán automáticamente.

El archivo `AGENTS.md` de la raíz indica cómo encontrar los workflows. Cuando se utilice otro agente, se le debe indicar expresamente que lea las instrucciones pertinentes.

Los workflows deben usar Markdown estándar y evitar dependencias innecesarias de un proveedor de IA.

## Fuentes del perfil profesional

`knowledge/cv_inicial.md` es el registro inmutable de la extracción original y la referencia histórica para rastrear el CV fuente.

`knowledge/cv_final.md` es el perfil enriquecido y la fuente canónica para los workflows posteriores.

Los workflows posteriores pueden consultar ambos documentos según su propósito, pero no deben modificar `cv_inicial.md`. `cv_final.md` solo puede actualizarse mediante un procedimiento que lo autorice expresamente y después de que el usuario apruebe los cambios concretos. `job-application` permite añadir datos nuevos confirmados bajo esa condición; `update-cv-profile` permite otras actualizaciones revisadas. Los demás resultados deben guardarse en artefactos derivados con nombres y propósitos específicos.

La corrección de `cv_inicial.md` o la actualización de `cv_final.md` requieren autorización explícita del usuario y un procedimiento independiente.
