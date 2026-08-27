# Bitácora de supervivencia — CitasSalud+

**Estudiante:** Alejandro_González_Beita
**Sección:** 11-6
**Fecha:** 27/08/2026

## Escenario

Durante la ejecución de la prueba de performance (JMeter, listado de citas con
500 registros simulados — ver Anexo 1), el servidor principal de CitasSalud+
se satura y queda fuera de línea.

## 1. Identificación

<!-- ¿Cómo se detectó que el servidor había caído? ¿Qué señal o dato lo evidenció? -->

La caída del servidor se detectó durante la prueba de carga de JMeter porque el listado de citas dejó de responder correctamente y las solicitudes comenzaron a fallar. La señal principal fue la indisponibilidad del servidor y el aumento de errores en las solicitudes realizadas durante la prueba con 500 registros.

## 2. Contención

<!-- ¿Qué acción se tomó de inmediato para limitar el impacto? -->

Como acción inmediata, se restringió temporalmente el acceso al módulo de listado de citas para evitar que nuevas solicitudes continuaran saturando el servidor. De esta manera se limitó el impacto sobre el resto de la aplicación y se evitó agravar la caída del servicio.

## 3. Recuperación

<!-- ¿Qué acción concreta permitió que la aplicación siguiera operando para
     citas de emergencia? Esta acción debe reflejarse en un commit de este
     repositorio con un mensaje descriptivo. -->

Para mantener operativa la aplicación para citas de emergencia, se activó un modo de solo emergencias, deshabilitando temporalmente las funciones no esenciales del listado de citas mientras se recuperaba el servidor. Esto permitió conservar la funcionalidad necesaria para atender citas de emergencia sin someter nuevamente al servidor a la carga que provocó la caída.

**Commit de recuperación:** Activa modo solo-emergencias mientras se optimiza el listado de citas

## 4. Aprendizaje / mejora

<!-- ¿Qué estrategia complementaria (respaldo, redundancia o monitoreo)
     hubiera anticipado este resultado, en relación con el criterio de
     performance del Anexo 1 (listado de citas en menos de 3 segundos)? -->

Como estrategia complementaria, se propone implementar monitoreo de rendimiento y disponibilidad del servidor junto con redundancia o un servidor de respaldo. Además, el listado debería probarse con cargas progresivas antes de pasar a producción y contar con paginación y límites de registros. Estas medidas permitirían detectar anticipadamente una degradación del servicio y verificar el cumplimiento del criterio del Anexo 1: mostrar el listado de citas en menos de 3 segundos para 500 registros.