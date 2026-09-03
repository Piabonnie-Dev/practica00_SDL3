# Práctica 00 — Reporte

Elliot Kenneth Villafana Pasten 118006642

## Plataforma
Windows con MSYS2, terminal UCRT64.

## Instalación
Las herramientas se instalaron desde la terminal MSYS2 UCRT64 con:

```
pacman -Syu
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-clang git mingw-w64-ucrt-x86_64-cmake pkgconf
```

## Versiones instaladas

### g++ --version
```
g++.exe (Rev3, Built by MSYS2 project) 16.2.0
Copyright (C) 2026 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

### clang++ --version
```
clang version 22.1.8 (https://github.com/msys2/MINGW-packages 6e4e79c2f86eeb534e324e583f2057dc9fd5ecab)
Target: x86_64-w64-windows-gnu
Thread model: posix
InstalledDir: C:/msys64/ucrt64/bin
```

### git --version
```
git version 2.55.0
```

### cmake --version
```
cmake version 4.4.2

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

## Comandos usados

```bash
g++ -std=c++17 basic.cpp -o basic.out.exe
./basic.out.exe
git init
git add .
git commit -m "Practica 0: basic.cpp y binario"
```

## Incidencias y soluciones

- **cmake no generaba salida ni con `--version`**: se diagnosticó con `which cmake`
  y `pacman -Qs cmake`, confirmando que el binario sí estaba instalado y en el
  PATH. El error real apareció al capturar stderr: faltaba la biblioteca
  dinámica `libjsoncpp-27.dll`. Se resolvió reinstalando la dependencia con:

  ```bash
  pacman -S mingw-w64-ucrt-x86_64-jsoncpp
  ```

  Tras esto, `cmake --version` funcionó correctamente (versión 4.4.2).

- **VS Code detectaba `cl.exe` (Visual Studio) en lugar de `g++`** al usar el
  botón de ejecución integrado (▷). Se resolvió compilando manualmente por
  terminal y mediante la tarea personalizada en `tasks.json`, que apunta
  explícitamente a `C:\msys64\ucrt64\bin\g++.exe`.
