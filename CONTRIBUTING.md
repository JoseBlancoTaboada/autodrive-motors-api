# Cómo trabajamos en este repositorio

Flujo corto y fijo para que los dos trabajemos en paralelo sin pisarnos.
El reparto de tareas está en [docs/PLAN-DE-TRABAJO.md](docs/PLAN-DE-TRABAJO.md).

## Reglas

1. **Nadie sube directo a `main`.** `main` está protegida: todo entra por
   Pull Request con la aprobación del otro.
2. **Una issue → una rama → un PR.** El PR dice `Closes #<número>` para
   que la issue se cierre sola al aceptarlo.
3. **Ramas cortas.** Mejor un PR chico por día que uno gigante al final:
   se revisa más rápido y hay menos conflictos.
4. **Se revisa en menos de 24 horas.** Si no se puede, se avisa en el PR.
5. **No se suben secretos.** Contraseñas y URL de la base van en variables
   de entorno o en `application-local.properties` (ignorado por git).

## Primera vez

```bash
git clone https://github.com/JoseBlancoTaboada/autodrive-motors-api.git
cd autodrive-motors-api
git config user.name "Tu Nombre"
git config user.email "tu-correo@ejemplo.com"
```

## Cada tarea

```bash
# 1. Partir siempre de main actualizado
git switch main
git pull

# 2. Rama con el número de la issue: tipo/numero-descripcion
git switch -c feat/9-ventas

# 3. Trabajar y hacer commits pequeños
git add .
git commit -m "feat(ventas): calcula el total con descuento del 5 %"

# 4. Subir la rama
git push -u origin feat/9-ventas

# 5. Abrir el PR (o desde la página del repo, botón "Compare & pull request")
gh pr create --fill --base main
```

Tipos de rama y de commit: `feat` (funcionalidad), `fix` (corrección),
`docs` (documentación y diagramas), `test` (pruebas o Postman), `chore`
(configuración). Ejemplos: `feat/8-clientes`, `docs/15-casos-de-uso`,
`test/19-postman-clientes-ventas`. No crear nunca una rama llamada solo
`feat` o `docs`: git no deja crear `feat/...` si existe `feat`.

## Revisar un PR del otro

En GitHub: pestaña **Files changed** → comentar las líneas → **Review
changes** → *Approve* o *Request changes*. Para probarlo en tu PC:

```bash
gh pr checkout <número>
./mvnw spring-boot:run
```

Qué mirar: que cumpla los criterios de la issue y la definición de
terminado del plan, que use DTO y validaciones, que los errores salgan
con el formato común, y que los pedidos de Postman funcionen.

## Aceptar el PR

Cuando está aprobado y el check de GitHub Actions está en verde: botón
**Squash and merge** (deja un solo commit limpio en `main`). La rama se
borra sola.

## Si `main` avanzó mientras trabajabas

```bash
git switch main
git pull
git switch feat/9-ventas
git merge main          # si hay conflictos, git marca los archivos
# resolver los conflictos en el editor, después:
git add .
git commit
git push
```

## Postman sin conflictos

Cada persona tiene **su propia colección** en `postman/` (un archivo
JSON cada uno) y comparten el entorno `postman/AutoDrive.postman_environment.json`
(con `baseUrl`). Dos personas editando el mismo JSON de Postman siempre
termina en conflicto.

## Diagramas

Van en `docs/diagramas/` como `.drawio` (la fuente, editable) **y**
`.png` (para el documento). Reglas de notación en
[docs/GUIA-UML.md](docs/GUIA-UML.md).
