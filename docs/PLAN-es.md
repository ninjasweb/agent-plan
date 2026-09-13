# Template de Plan — SDD + TDD

Este archivo es la referencia obligatoria para crear planes de trabajo. Combina **Spec-Driven Development (SDD)** para decidir qué debe hacer el sistema con **Test-Driven Development (TDD)** para demostrarlo durante la implementación.

## Cómo usar este template

1. No conviertas `PLAN.md` en un plan concreto ni lo sobrescribas.
2. Crea un archivo hermano llamado `PLAN-<tema>.md`, con un slug corto y descriptivo en kebab-case; por ejemplo, `PLAN-payment-idempotency.md`.
3. Si ya existe un plan activo para el mismo objetivo, actualízalo en vez de duplicarlo.
4. Mantén el plan activo en `docs/`. Al terminarlo, muévelo a la subcarpeta temática correspondiente.
5. Elimina del plan creado estas instrucciones y cualquier sección que no aplique.

## Relación entre SDD y TDD

La especificación es la fuente de verdad. Cada test debe derivarse de un criterio de aceptación y cada cambio de producción debe estar justificado por un test o una verificación explícita.

```text
Historia → asunciones validadas → requisitos → criterios de aceptación
        → tests → RED → GREEN → REFACTOR → evidencia
```

No dupliques reglas de negocio entre la especificación y la sección de pruebas: usa IDs y trazabilidad.

## Gates del proceso

- **Gate 1 — SPEC READY:** alcance, asunciones, requisitos y criterios de aceptación están validados.
- **Gate 2 — TEST READY:** cada criterio está mapeado a una prueba o verificación justificable.
- **Gate 3 — SLICE DONE:** el corte completó RED → GREEN → REFACTOR y pasó sus checks.
- **Gate 4 — PLAN DONE:** todos los criterios tienen evidencia y no quedan regresiones conocidas.

---

# PLAN: [Título concreto]

> Creado a partir de `docs/PLAN.md`. La especificación define el comportamiento; los tests lo demuestran.

## 0. Control del documento

| Campo             | Valor                                                                     |
| ----------------- | ------------------------------------------------------------------------- |
| Archivo           | `docs/PLAN-[tema].md`                                                     |
| Estado            | Borrador / En refinamiento / Aprobado / En curso / Bloqueado / Completado |
| Autor / owner     | [Nombre o equipo]                                                         |
| Creado            | YYYY-MM-DD                                                                |
| Actualizado       | YYYY-MM-DD                                                                |
| Rama / issue / PR | [Enlaces o N/A]                                                           |

## 1. Contexto y problema

### Situación actual

[Describe el comportamiento actual con evidencia verificable: código, logs, métricas, capturas o pasos de reproducción.]

### Problema

[Explica quién se ve afectado, qué falla o falta y cuál es el impacto.]

### Resultado esperado

[Describe el cambio observable que indicará que el problema está resuelto.]

## 2. Historia de usuario

> Como **[actor]**, quiero **[acción/capacidad]**, para **[beneficio medible]**.

### Historias relacionadas

- US-001: Como [actor], quiero [acción], para [beneficio].

## 3. Objetivos y límites

### Objetivos

- O-001: [Resultado concreto y verificable.]

### En alcance

- [Comportamiento incluido.]

### Fuera de alcance

- [Comportamiento excluido explícitamente.]

## 4. Asunciones funcionales y decisiones

Antes de cerrar la especificación, listar las asunciones funcionales atómicas y refinarlas con el usuario. No esconder decisiones de producto dentro de la estrategia técnica.

| ID    | Asunción o decisión            | Estado                           | Evidencia / decisión |
| ----- | ------------------------------ | -------------------------------- | -------------------- |
| A-001 | [Una sola asunción funcional.] | Pendiente / Validada / Rechazada | [Fuente o respuesta] |

### Preguntas abiertas

- Q-001: [Pregunta que bloquea una decisión material.]

**Gate 1 no puede aprobarse mientras una pregunta material siga abierta.**

## 5. Especificación SDD

### Actores y permisos

| Actor   | Puede                 | No puede        |
| ------- | --------------------- | --------------- |
| [Actor] | [Acciones permitidas] | [Restricciones] |

### Requisitos funcionales

Cada requisito debe ser atómico, obligatorio y observable.

| ID     | Requisito                                     | Prioridad             | Origen |
| ------ | --------------------------------------------- | --------------------- | ------ |
| FR-001 | El sistema debe [comportamiento verificable]. | Must / Should / Could | US-001 |

### Criterios de aceptación

#### AC-001 — [Nombre del escenario]

- **Dado** [estado inicial]
- **Cuando** [acción o evento]
- **Entonces** [resultado observable]
- **Y** [resultado adicional, si aplica]

#### AC-002 — [Error o caso límite]

- **Dado** [estado inicial]
- **Cuando** [acción inválida, fallo o concurrencia]
- **Entonces** [respuesta segura y observable]

### Requisitos no funcionales

Usar umbrales medibles; omitir categorías que no apliquen.

| ID      | Categoría                                               | Requisito / umbral | Cómo se verifica       |
| ------- | ------------------------------------------------------- | ------------------ | ---------------------- |
| NFR-001 | Rendimiento / Seguridad / Accesibilidad / Confiabilidad | [Métrica concreta] | [Herramienta o prueba] |

### UX y estados visibles

- Entrada o trigger: [Dónde empieza el flujo.]
- Loading/progreso: [Qué ve el usuario.]
- Éxito: [Feedback y siguiente estado.]
- Vacío: [Comportamiento sin datos.]
- Error recuperable: [Mensaje y acción disponible.]
- Error definitivo: [Mensaje, preservación de datos y soporte.]
- Accesibilidad/localización: [Requisitos aplicables.]

### Datos, contratos y efectos secundarios

| Elemento                             | Estado actual     | Cambio requerido    | Compatibilidad / migración |
| ------------------------------------ | ----------------- | ------------------- | -------------------------- |
| [Modelo, endpoint, evento o storage] | [Contrato actual] | [Contrato objetivo] | [Estrategia]               |

### Casos límite y errores

| ID       | Caso                                             | Comportamiento esperado | Criterio relacionado |
| -------- | ------------------------------------------------ | ----------------------- | -------------------- |
| EDGE-001 | [Duplicado, timeout, input vacío, carrera, etc.] | [Resultado seguro]      | AC-002               |

## 6. Estrategia técnica

Definir esta sección después de estabilizar el comportamiento funcional.

### Arquitectura actual relevante

[Resumen del flujo confirmado en el código; incluir rutas y símbolos reales.]

### Diseño propuesto

[Componentes, límites, flujo de datos y decisiones técnicas mínimas.]

### Archivos previstos

| Archivo / módulo | Acción                       | Responsabilidad del cambio |
| ---------------- | ---------------------------- | -------------------------- |
| `[ruta]`         | Crear / Modificar / Eliminar | [Propósito]                |

### Dependencias y restricciones

- [Dependencia interna/externa, compatibilidad, migración o limitación operativa.]

## 7. Matriz de trazabilidad

No debe haber requisitos huérfanos ni tests sin comportamiento especificado.

| Historia / objetivo | Requisito | Criterio | Test / verificación | Corte |
| ------------------- | --------- | -------- | ------------------- | ----- |
| US-001 / O-001      | FR-001    | AC-001   | TEST-001            | S1    |

## 8. Estrategia TDD

### Línea base y caracterización

- Tests existentes relevantes: [rutas y estado].
- Comando baseline: `[comando]`.
- Resultado baseline: [evidencia].
- Si el comportamiento existente no está cubierto, crear primero tests de caracterización antes de refactorizarlo.
- Para un bug, reproducirlo primero con un test de regresión que falle por la razón correcta.

### Inventario de tests

| ID       | Criterio | Nivel                                | Escenario        | Archivo previsto | Estado                  |
| -------- | -------- | ------------------------------------ | ---------------- | ---------------- | ----------------------- |
| TEST-001 | AC-001   | Unit / Integration / Component / E2E | [Comportamiento] | `[ruta]`         | Pendiente / RED / GREEN |

### Reglas TDD

- Ejecutar un ciclo **RED → GREEN → REFACTOR** por corte pequeño.
- Confirmar que RED falla por ausencia del comportamiento, no por configuración rota.
- Escribir la implementación mínima que lleve GREEN; no anticipar requisitos futuros.
- Refactorizar solo con la suite en verde y volver a ejecutarla después.
- Probar comportamiento observable, no detalles privados de implementación.
- Usar integración en límites críticos; mockear únicamente fronteras externas cuando sea necesario.
- No omitir, debilitar ni borrar un test para conseguir GREEN sin documentar una corrección de la especificación.
- Si TDD no aplica —documentación, configuración declarativa, migración no reversible o spike— registrar la razón y una verificación equivalente antes de implementar.

## 9. Cortes de implementación

Repetir esta estructura para cada corte vertical. Un corte debe entregar un comportamiento verificable, no solo una capa técnica.

### S1 — [Resultado pequeño y observable]

- Requisitos: FR-001
- Criterios: AC-001
- Tests: TEST-001
- Dependencias: [Ninguna o IDs previos]

#### RED

- [ ] Crear o modificar `[archivo de test]`.
- [ ] Ejecutar `[comando focalizado]`.
- [ ] Registrar el fallo esperado: [mensaje o condición].

#### GREEN

- [ ] Implementar el cambio mínimo en `[archivo(s)]`.
- [ ] Ejecutar `[comando focalizado]` hasta pasar.
- [ ] Ejecutar pruebas relacionadas para descartar regresiones inmediatas.

#### REFACTOR

- [ ] Eliminar duplicación y mejorar nombres/límites sin cambiar comportamiento.
- [ ] Reejecutar tests focalizados y suite relevante.
- [ ] Actualizar trazabilidad, decisiones y documentación afectada.

#### Gate del corte

- [ ] RED fue observado y registrado.
- [ ] GREEN pasa de forma reproducible.
- [ ] El refactor conserva GREEN.
- [ ] No quedan errores de tipos, lint o formato en el alcance.

### S2 — [Siguiente resultado]

[Repetir RED → GREEN → REFACTOR.]

## 10. Validación integral

### Comandos

```bash
# Test focalizado
[comando]

# Suite relacionada
[comando]

# Tipos / lint / build, según riesgo
[comando]
```

### Verificación manual

| Escenario                               | Pasos                 | Resultado esperado | Evidencia     |
| --------------------------------------- | --------------------- | ------------------ | ------------- |
| [Escenario no cubierto automáticamente] | [Pasos reproducibles] | [Resultado]        | [Captura/log] |

## 11. Rollout, observabilidad y rollback

- Estrategia de despliegue: [directo, gradual, feature flag, migración].
- Métricas/logs/alertas: [señales concretas y umbrales].
- Compatibilidad: [versiones o clientes afectados].
- Rollback: [pasos seguros y condición para activarlo].
- Datos: [reversibilidad, respaldo y reconciliación].

## 12. Riesgos

| Riesgo   | Probabilidad        | Impacto             | Mitigación | Señal temprana  |
| -------- | ------------------- | ------------------- | ---------- | --------------- |
| [Riesgo] | Baja / Media / Alta | Bajo / Medio / Alto | [Acción]   | [Métrica/error] |

## 13. Registro de decisiones y progreso

### Decisiones

| Fecha      | ID    | Decisión   | Motivo      | Consecuencia |
| ---------- | ----- | ---------- | ----------- | ------------ |
| YYYY-MM-DD | D-001 | [Decisión] | [Evidencia] | [Trade-off]  |

### Progreso

| Fecha      | Corte | Estado                        | Evidencia           | Siguiente paso |
| ---------- | ----- | ----------------------------- | ------------------- | -------------- |
| YYYY-MM-DD | S1    | RED / GREEN / REFACTOR / Done | [Comando/resultado] | [Acción]       |

## 14. Definition of Done

- [ ] Gate 1 — SPEC READY aprobado.
- [ ] Gate 2 — TEST READY aprobado.
- [ ] Todos los cortes completaron RED → GREEN → REFACTOR.
- [ ] Todos los `FR-*` trazan a `AC-*` y a `TEST-*` o a una verificación justificada.
- [ ] Happy path, errores y casos límite críticos están cubiertos.
- [ ] Tests focalizados y suite relacionada pasan.
- [ ] Typecheck, lint y build aplicables pasan.
- [ ] No hay tests deshabilitados ni regresiones conocidas sin documentar.
- [ ] Observabilidad y rollback están listos según el riesgo.
- [ ] Documentación y `FLOWS.md` fueron actualizados cuando aplica.
- [ ] La evidencia final está registrada en este plan.

## 15. Resultado final

- Estado: [Completado / Parcial / Bloqueado]
- Evidencia: [tests, métricas, capturas o enlaces]
- Desviaciones respecto a la spec: [ninguna o decisiones `D-*`]
- Trabajo posterior: [ninguno o items explícitos fuera de alcance]
