# Prueba limpia del juego PC con motor portable - 17/11/2026

## Qué se probó
- Instalación aislada creada **únicamente a partir de los 17 ZIP** preparados para la release QA, sin reutilizar directorios ni junctions de la instalación jugable de PC2.
- Se extrajeron 19.413 archivos (5.683.197.912 bytes), verificando el SHA-256 de cada archivo extraído contra `files.json`. Resultado: **17/17 ZIP y 19.413/19.413 archivos correctos**.
- Arranque con el ejecutable `hl2_launcher.exe` extraído de esos ZIP, desde su propia carpeta, argumentos `-game tf_port -insecure -nosteam -multirun -novid -windowed -w 1100 -h 700 -console -condebug -dev -dxlevel 95 -port 27125 -clientport 27126 +sv_lan 1 +maxplayers 8 +tf_bot_quota 0 +map ctf_2fort +path`.
- El motor inició, abrió una ventana, cargó el mapa `ctf_2fort`, levantó servidor local UDP 27125, registró `unnamed connected` y presentó las pantallas gráficas de bienvenida e instrucciones de 2Fort.
- En `engine.log` se verificó `filesystem BaseDir` correspondiente a la carpeta de prueba, además de rutas VPK `hl2/*.vpk` y `platform/*.vpk` apuntando a esa misma carpeta. Los archivos físicos tienen sufijos `_dir.vpk` y `_000.vpk` etc.; **el motor los montó desde el propio paquete**.
- Inspección de 122 módulos con PowerShell de 32 bits: `engine.dll`, `client.dll`, `server.dll`, `materialsystem.dll`, `filesystem_stdio.dll`, `stdshader_dx9.dll` y `steam_api.dll` cargados desde la carpeta aislada. **0 módulos cargados desde el directorio de Steam o de Source SDK Base 2013 Multiplayer**.

## Limitaciones verificadas
- El video introductorio del mapa quedó en blanco y el intento de salir de esa pantalla no permitió entrar a controlar un personaje. Por lo tanto **NO se certificó movimiento/HUD dentro de la partida**. Las instrucciones y el mapa se muestran, pero no se concluye jugabilidad completa.
- `engine.log`: `Unable to load voice codec 'vaudio_opus'. Voice disabled`. Faltan componentes de voz o compatibilidad; no se atribuye causa exacta todavía.
- Hay avisos de shaders/materiales y recursos táctiles `vgui/touch/*` faltantes. Están documentados, sin corregir a ciegas.
- La prueba se hizo con `-nosteam`, y el motor anunció modo LAN sin biblioteca de soporte Steam. **PC2 sí tiene Source SDK Base instalado**, por lo que aunque no se observó uso de sus DLL o VPK, esto no sustituye una prueba en otra PC que carezca completamente de Steam/SDK.
- Esto demuestra que el runtime/motor necesario está empaquetado; **no incluye un SDK de desarrollo completo** (Hammer, compiladores de mapas, código fuente).

## Evidencia en PC2
- Carpeta limpia: `C:\TF2AndroidLAN\PC_PREPARADO_PARA_SUBIR_NO_PUBLICAR_20261116\QA_INSTALACION_LIMPIA_MOTOR_INTERNO_20261117`
- Extracción: `QA_TEST_SDK_INTERNO_PROGRESS.json`, `QA_TEST_SDK_EXTRACT_LOG.txt`.
- Registro del motor: `QA_INSTALACION_LIMPIA_MOTOR_INTERNO_20261117\engine.log` y `tf_port\console.log`.
- Capturas: `QA_INSTALACION_LIMPIA_2FORT_CONNECTED_20261117.jpg`, `QA_CLEAN_MAP_CLASS_MENU_20261117.jpg`, `QA_CLEAN_POST_CLASS_ATTEMPT_20261117.jpg`.
- Solo se cerró el proceso de prueba 11340; la instalación principal de PC2 (proceso 8492 en UDP 27025) quedó funcionando.

**Resultado QA:** arranque portable, montaje de recursos y carga del mapa confirmados; controles jugables, intro y voz no validados como completos.
