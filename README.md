# AutoDrive Motors — API REST de gestión vehicular

Taller final de **Análisis y Diseño de Software**. API RESTful en Spring
Boot para la gestión de clientes, vehículos, ventas y mantenimientos de la
empresa AutoDrive Motors, con base de datos relacional, consumo de una API
externa de tasas de cambio (COP → USD) y pruebas en Postman.

- Reparto del trabajo: [docs/PLAN-DE-TRABAJO.md](docs/PLAN-DE-TRABAJO.md)
- Cómo trabajamos con git y GitHub: [CONTRIBUTING.md](CONTRIBUTING.md)
- Reglas de los diagramas: [docs/GUIA-UML.md](docs/GUIA-UML.md)
- Tareas: pestaña **Issues** (filtrar por la etiqueta `persona-a` o `persona-b`)

## Equipo

| Rol en el plan | Integrante | GitHub |
|---|---|---|
| Persona A | José Blanco | @JoseBlancoTaboada |
| Persona B | _(por definir)_ | _(por definir)_ |

## Qué hay que entregar (enunciado)

| # | Entregable | Dónde queda |
|---|---|---|
| 1 | API REST funcionando | `src/` |
| 2 | Base de datos relacional conectada (MySQL o PostgreSQL) | `src/main/resources/` |
| 3 | Relaciones entre entidades (JPA) | `src/.../entity/` |
| 4 | CRUD completos | `src/.../controller/`, `service/` |
| 5 | Validaciones | DTO + servicios |
| 6 | Consumo de API externa (tasa de cambio) | `src/.../client/` |
| 7 | Pruebas en Postman | `postman/` |
| 8 | Arquitectura por capas | paquetes `controller`, `service`, `repository`… |
| 9 | Manejo de excepciones | `src/.../exception/` |
| 10 | DTOs | `src/.../dto/` |
| 11 | Documentación UML y DER | `docs/diagramas/` |
| — | Requerimientos funcionales y no funcionales, historias de usuario | `docs/requerimientos/` |

### Reglas de negocio

1. No se puede vender un vehículo vendido o en mantenimiento.
2. No se permiten precios negativos.
3. La placa del vehículo es única.
4. No se repiten correos de clientes.
5. Toda venta genera automáticamente su fecha y su total.
6. Si el valor del vehículo supera $100.000.000 COP, se aplica un 5 % de descuento.

### Endpoints mínimos

| Recurso | Endpoints |
|---|---|
| Clientes | `GET /clientes`, `POST /clientes`, `PUT /clientes/{id}`, `DELETE /clientes/{id}` |
| Vehículos | `GET /vehiculos`, `POST /vehiculos`, `GET /vehiculos/disponibles`, `GET /vehiculos/marca/{marca}` |
| Ventas | `POST /ventas`, `GET /ventas` |
| Mantenimientos | `POST /mantenimientos`, `GET /mantenimientos` |

## Cómo correrlo

_Se completa en la issue "README final e instrucciones de ejecución"_:
requisitos (JDK, base de datos), variables de entorno, cómo crear la base,
`./mvnw spring-boot:run` y cómo importar las colecciones de Postman.
