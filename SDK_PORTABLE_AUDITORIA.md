# Motor y SDK portable: resultado de la revisión (17/11/2026)

## Qué viene incluido para ejecutar TF2 PC

El paquete de PC contiene estos archivos, controlados por `files.json` y sus SHA-256:

- `hl2_launcher.exe` (inicia el juego).
- `bin/engine.dll` y las bibliotecas del motor Source para Windows.
- `tf_port/bin/client.dll` y `tf_port/bin/server.dll` (código compilado del juego).
- `bin/stdshader_dx9.dll` (se usa la versión del HUD recuperado, hash `519286e2b503c41163ebdd1e5669b0ba0e93d005a05fda5bfaf382267972ad76`).
- Contenido compartido `hl2/`, `platform/`, mapas, materiales, modelos y sonidos.

`tf_port/gameinfo.txt` declara `SteamAppId 243750` (Source SDK Base 2013 Multiplayer) y monta archivos VPK compartidos que YA están incluidos en el paquete PC.

**Conclusión comprobada:** están incluidos los archivos de ejecución del motor, por lo que no hay que descargar por separado los VPK o DLL de esa base para completar este paquete. No implica que estén garantizados Steam offline, VAC, autenticación o todas las funciones del SDK.

## Qué NO está incluido

No hay directorios de código fuente ni herramientas del SDK de desarrollo completo como proyectos compilables, Hammer, compiladores de mapas o herramientas de depuración. Existe un árbol de código fuente en PC2, pero está afuera del paquete, en:

`C:\TF2AndroidLAN\PayloadQA25\src`

No se lo mezcla automáticamente con la carpeta de instalación del jugador: no hace falta para jugar y debe revisarse por separado antes de crear un paquete para desarrolladores.

## Estado de pruebas

El paquete que se publica corresponde a la base editable, no a la build experimental de PC2. `client.dll`, `server.dll` y `hl2_launcher.exe` difieren de la build experimental. Hay que seguir verificando luces, materiales y el error `Server uses different class tables` con Android. Esta publicación es QA, no estable.
