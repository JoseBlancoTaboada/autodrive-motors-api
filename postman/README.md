# Colecciones de Postman

Una colección por persona, para no editar los dos el mismo JSON:

| Archivo | Responsable | Contenido |
|---|---|---|
| `clientes-ventas.postman_collection.json` | Persona A | Clientes (CRUD) y Ventas, con casos de error (correo repetido, vehículo vendido o en mantenimiento, descuento > $100.000.000) |
| `vehiculos-mantenimientos.postman_collection.json` | Persona B | Vehículos (CRUD, disponibles, por marca), Mantenimientos y precio en USD, con casos de error (placa repetida, precio negativo) |
| `AutoDrive.postman_environment.json` | Compartido | Variable `baseUrl` (por ejemplo `http://localhost:8080`) |

En Postman: *Import* → elegir los tres archivos → seleccionar el entorno
"AutoDrive" arriba a la derecha. Para exportar después de cambiar algo:
clic derecho en la colección → *Export* → v2.1, y guardar encima del
archivo de esta carpeta.
