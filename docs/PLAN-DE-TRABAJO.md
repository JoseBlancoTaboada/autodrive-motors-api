# Plan de trabajo — AutoDrive Motors (Taller final)

Asignatura: Análisis y Diseño de Software. Equipo de dos: **Persona A** y
**Persona B**. Este plan reparte el taller de forma que cada uno haga la
misma cantidad de trabajo **y** toque todas las partes (backend, base de
datos, UML, documentación y pruebas), porque los dos tienen que poder
explicar el proyecto completo.

## Cómo se reparte (y por qué así)

1. **Por módulos verticales, no por capas.** Cada persona es dueña de
   módulos completos, de punta a punta: entidad, repositorio, servicio,
   DTO, controlador, validaciones, colección de Postman y el diagrama de
   secuencia de su flujo. Repartir por capas ("yo hago controladores, tú
   haces servicios") hace que uno espere al otro todo el tiempo.
2. **Por puntos, no por cantidad de tareas.** Cada tarea tiene puntos de
   esfuerzo (1 = muy chica … 8 = la más grande). Los totales quedan
   parejos: **A = 38 puntos, B = 37 puntos**.
3. **Con revisión cruzada.** Nada entra a `main` sin que el otro lo
   revise y apruebe en un Pull Request. Así los dos conocen todo el código
   y queda escrito quién hizo qué.
4. **Todo se ve en GitHub.** Cada tarea es una issue asignada; cada PR
   cierra su issue (`Closes #n`). El historial de commits, las issues
   cerradas y los PR revisados muestran el aporte de cada uno sin
   discusiones.

## Reparto

| Persona A (38 pts) | Persona B (37 pts) |
|---|---|
| Esqueleto Spring Boot y conexión a la base (3) | DER en notación de Chen (3) |
| Manejo global de excepciones y formato de error (3) | Modelo relacional (2) |
| Requerimientos funcionales (3) | Entidades JPA y relaciones (3) |
| Requerimientos no funcionales (2) | Vehículos: DTO, validaciones y endpoints (5) |
| Clientes: DTO, validaciones y CRUD (5) | Mantenimientos: registrar e historial (5) |
| **Ventas: reglas de negocio** (8) | API externa: tasa de cambio COP → USD (5) |
| Historias de usuario de Clientes y Ventas (2) | Historias de usuario de Vehículos y Mantenimientos (2) |
| Diagrama de casos de uso (3) | Diagrama de clases (3) |
| Diagrama de secuencia: Registrar venta (3) | Diagrama de secuencia: Consultar vehículo con precio en USD (3) |
| Postman: Clientes y Ventas (2) | Postman: Vehículos, Mantenimientos y tasa (2) |
| Prueba cruzada de los endpoints de B (2) | Prueba cruzada de los endpoints de A (2) |
| README final e instrucciones de ejecución (2) | Documento final de entrega (2) |

Por tipo de trabajo queda así: backend A 19 / B 18; documentación,
diagramas y base de datos A 15 / B 15; Postman y pruebas A 4 / B 4.

Si alguno prefiere el otro lado, se intercambia la columna entera (se
cambian las etiquetas `persona-a` y `persona-b` de las issues): el
equilibrio se mantiene.

## Etapas (hitos de GitHub)

| Hito | Qué se cierra | Regla |
|---|---|---|
| **Sprint 0 — Base común** | Esqueleto, excepciones, DER, modelo relacional, entidades, requerimientos | Primero que todo. Hasta que esté el esqueleto en `main`, B avanza con DER y modelo relacional (no necesitan código) |
| **Sprint 1 — Módulos** | Los cuatro módulos, la API externa, historias de usuario, los tres diagramas UML, Postman | Cada uno en su rama y su PR; se pueden hacer en paralelo |
| **Sprint 2 — Integración y entrega** | Pruebas cruzadas, README, documento final | Al final, con todo lo anterior en `main` |

Las fechas de cada hito las ponen ustedes según la fecha de entrega
(GitHub → Issues → Milestones → Edit).

## Contratos que se acuerdan en el Sprint 0

Para que nadie quede bloqueado esperando al otro, estos acuerdos se fijan
en las issues del Sprint 0 y después no se cambian sin avisar en la issue:

- **Entidades y nombres** (issue de entidades, B): `Cliente`, `Vehiculo`,
  `Venta`, `Mantenimiento`, el enum `EstadoVehiculo { DISPONIBLE, VENDIDO,
  EN_MANTENIMIENTO }`, y los nombres de sus campos.
- **Formato de error** (issue de excepciones, A): el JSON que devuelve
  cualquier error y qué código HTTP corresponde a cada caso.
- **Rutas**: las del enunciado (`/clientes`, `/vehiculos`,
  `/vehiculos/disponibles`, `/vehiculos/marca/{marca}`, `/ventas`,
  `/mantenimientos`).
- **Dinero**: `BigDecimal`, en pesos colombianos (COP).

A usa `Vehiculo` y `EstadoVehiculo` en Ventas; B usa el formato de error
en sus endpoints. Por eso esas dos issues van primero.

## Decisiones que el enunciado no resuelve

Anótenlas en la issue correspondiente cuando las decidan (y en el
documento final):

- ¿Cómo vuelve un vehículo de `EN_MANTENIMIENTO` a `DISPONIBLE`? (por
  ejemplo, finalizar el mantenimiento). Afecta a Ventas: se decide entre
  los dos.
- Descuento: "supera los $100.000.000" se interpreta como **estrictamente
  mayor** (`precio > 100.000.000` → 5 % de descuento).
- ¿Se puede eliminar un cliente o un vehículo que ya tiene ventas? (la
  base no debería dejar ventas huérfanas).
- Qué API pública de tasas se usa (tiene que incluir COP) y qué pasa si no
  responde.

## Definición de terminado (aplica a toda issue de código)

- [ ] El código está en una rama propia y entró a `main` por un PR
      aprobado por el otro.
- [ ] Usa DTO de entrada y de salida (nunca la entidad en el controlador).
- [ ] Valida la entrada (`@Valid` y anotaciones de Jakarta Validation) y
      aplica las reglas de negocio en el servicio.
- [ ] Los errores salen con el formato común (manejador global).
- [ ] Tiene sus pedidos en la colección de Postman, con casos que
      funcionan **y** casos de error.
- [ ] `./mvnw verify` pasa (lo corre GitHub Actions en cada PR).
- [ ] Si cambió algo del diseño, se actualizó el diagrama.

Para las issues de documentación y diagramas: el archivo está en `docs/`,
el otro lo revisó en el PR, y los diagramas siguen
[GUIA-UML.md](GUIA-UML.md).

## Si alguien se atrasa o termina antes

- Se avisa **en la issue** (comentario), no por chat: así queda escrito.
- Quien termina antes ayuda revisando PR o toma una issue del otro **solo
  si el otro está de acuerdo**; la issue se reasigna en GitHub para que
  conste.
- El aporte se ve en *Insights → Contributors*, en las issues cerradas
  por cada uno y en los PR revisados.

## Cierre

Antes de entregar, juntos: correr la API desde cero en una PC limpia
siguiendo el README, ejecutar las dos colecciones de Postman completas y
revisar que los diagramas coincidan con el código final.
