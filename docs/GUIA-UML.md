# Guía de diagramas del taller

El taller pide: **casos de uso, clases y secuencia** (UML) y **DER y
modelo relacional** (base de datos). Esta guía resume las reglas que más
se rompen, con la cláusula de la especificación oficial
[OMG UML 2.5.1](https://www.omg.org/spec/UML/2.5.1/PDF) que las define.
Antes de pedir revisión de un diagrama, pasar su lista.

## Para todos

- [ ] Los nombres son los mismos en todos los diagramas y en el código
      (`Vehiculo`, `EstadoVehiculo`, `VentaService`…).
- [ ] No hay formas inventadas: nada de cilindros, flechas de dos puntas,
      elipses punteadas ni cajas punteadas "para agrupar".
- [ ] Lo que no es parte de la notación va en una **nota** (rectángulo con
      la esquina doblada), no como texto suelto.
- [ ] Cada diagrama se entrega como `.drawio` + `.png` en `docs/diagramas/`.

## Casos de uso (UML 18)

- [ ] Actores **fuera** del límite del sistema; el nombre del sistema
      arriba a la izquierda del rectángulo.
- [ ] Persona → monigote con cabeza redonda. Sistema externo (la API de
      tasas de cambio) → monigote con **cabeza cuadrada** y `«system»`, o
      rectángulo con `«actor»`. Nunca el mismo monigote para los dos.
- [ ] Un actor es un rol ("Asesor de ventas", "Administrador"), no una
      persona.
- [ ] Asociación actor–caso: línea sólida sin flecha. Los actores no se
      unen entre sí.
- [ ] `«include»`: punteada con punta abierta **del caso base al
      incluido** (siempre pasa). Ej.: *Registrar venta* `«include»`
      *Calcular total de venta*.
- [ ] `«extend»`: punteada **del caso que extiende al extendido** (pasa
      solo si se cumple algo), con una nota `condition: {…}`. Ej.:
      *Aplicar descuento del 5 %* `«extend»` *Calcular total de venta*,
      `condition: {precio > 100.000.000}`.
- [ ] Nombres de casos = verbo + objeto ("Registrar mantenimiento").

## Clases (UML 9 y 11)

- [ ] Atributos: `- placa: String`, con visibilidad y tipo. En Java los
      atributos son `-` (private).
- [ ] Operaciones: `+ registrar(dto: VentaRequest): VentaResponse`, con
      parámetros `nombre: Tipo` y tipo de retorno.
- [ ] `+` public, `-` private, `#` protected, `~` package (Java sin
      modificador). Lo `static` va subrayado.
- [ ] Multiplicidad en **los dos** extremos de cada asociación
      (`Cliente 1 —— 0..* Venta`).
- [ ] Enum como clase con `«enumeration»` y sus valores.
- [ ] Rombo de composición o agregación pegado al **todo**, no a la parte
      (y solo si de verdad la parte depende del todo).
- [ ] Si se dibujan las capas: dependencias punteadas
      `Controller → Service → Repository`, nunca al revés.

## Secuencia (UML 17)

- [ ] Marco `sd Registrar venta` alrededor de todo.
- [ ] Cabeceras `:VentaController`, `:VentaService`, `:VehiculoRepository`
      (nombre: Tipo, sin subrayar). El actor como monigote.
- [ ] Llamada = línea sólida con punta llena; respuesta = línea
      **punteada** que vuelve **a quien llamó** (no salta niveles).
- [ ] Activaciones (rectángulos angostos) mientras cada uno trabaja.
- [ ] Reglas de negocio con fragmentos: `alt [vehículo VENDIDO o
      EN_MANTENIMIENTO]` / `[else]`, `opt [precio > 100.000.000]`.
- [ ] Un diagrama = un escenario.

## DER (Chen 1976; Elmasri & Navathe, fig. 3.14)

- [ ] Entidad = rectángulo, relación = **rombo** con un verbo, atributo =
      óvalo, clave **subrayada**.
- [ ] Cardinalidad `1`, `N`, `M` en cada línea de cada relación;
      participación total con línea doble.
- [ ] Sin claves foráneas: en el DER la relación es el rombo.
- [ ] Atributos calculados (total de la venta) con óvalo punteado o fuera.
- [ ] No mezclar con la notación de pata de gallo.

## Modelo relacional (Codd 1970; Elmasri & Navathe, cap. 9)

- [ ] Cada entidad es una tabla; PK subrayada.
- [ ] Relación 1:N → la PK del lado 1 va como **FK en la tabla del lado N**
      (`VENTA.id_cliente`, `VENTA.id_vehiculo`, `MANTENIMIENTO.id_vehiculo`).
- [ ] Relación M:N → tabla intermedia con las dos FK.
- [ ] Las reglas del enunciado se ven en el modelo: `placa UNIQUE`,
      `correo UNIQUE`, `precio CHECK (precio >= 0)`.
- [ ] Coincide con el DER y con las entidades JPA.

## Herramienta

draw.io (app de escritorio o diagrams.net). Formas útiles: en el panel
"UML" están el actor, el caso de uso, la clase y la línea de vida; para el
DER, el panel "Entity Relation". Para la cabeza cuadrada del actor de
sistema: un rectángulo chico de 20×20 sobre el cuerpo del monigote, o el
rectángulo con `«actor»`.
