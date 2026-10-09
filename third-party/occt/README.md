# OCCT 7.9.3 — corresponding source / fuente correspondiente

This directory provides the official Open CASCADE Technology 7.9.3 source archive used for the rebuilt TKTopAlgo DLL distributed with Mesh2Solid 0.1.0. The source is unmodified. The rebuild changes compiler options to avoid a native crash in the original MSYS2 binary.

Esta carpeta ofrece la fuente oficial de Open CASCADE Technology 7.9.3 utilizada para recompilar la DLL TKTopAlgo distribuida con Mesh2Solid 0.1.0. No se modifica la fuente; se cambian opciones de compilación para evitar un cierre nativo del binario MSYS2 original.

- [Download source / Descargar fuente](https://github.com/Qualith/Mesh2Solid/raw/refs/heads/main/third-party/occt/occt-7.9.3-source.tar.gz)
- SHA256: `5ecf094ec6b12d5413dfb851d8c3590c354058aee556e32e408bdfbf8c357d57`
- Original archive / Archivo original: https://codeload.github.com/Open-Cascade-SAS/OCCT/tar.gz/refs/tags/V7_9_3
- Licence / Licencia: LGPL 2.1 with the Open CASCADE exception. The archive contains `LICENSE_LGPL_21.txt` and `OCCT_LGPL_EXCEPTION.txt`; the application package also includes these licence notices.

## Rebuild / Recompilación

Only TKTopAlgo is rebuilt. The bundled `CMakeLists.txt` is the compilation recipe used by Mesh2Solid; it is a subdirectory recipe, not a standalone project. It compiles the packages listed in `src/TKTopAlgo/PACKAGES`, using the unmodified sources and include directories from the archive, and links against the other pinned OCCT modules.

Solo se recompila TKTopAlgo. El `CMakeLists.txt` incluido es la receta utilizada por Mesh2Solid: pertenece a un subdirectorio del proyecto, no es un proyecto independiente. Compila los paquetes de `src/TKTopAlgo/PACKAGES`, con las fuentes y cabeceras originales del archivo, y enlaza con los demás módulos OCCT fijados.

The verified toolchain / Cadena verificada: Windows x64, MSYS2 UCRT64, GCC 16.2.0, CMake 4.4.4, Ninja 1.13.2, OCCT 7.9.3 (`mingw-w64-ucrt-x86_64-opencascade-7.9.3-3`).

Extract the archive as `.tools/OCCT-7_9_3` relative to the main CMake project. The recipe expects the OpenCASCADE include and library directories from `find_package(OpenCASCADE 7.9.3 EXACT REQUIRED)` and the MSYS2 OCCT runtime. Compile the `m2s_occt_topalgo` shared-library target and place its output beside the other runtime DLLs as `libTKTopAlgo.dll`.

Extrae el archivo como `.tools/OCCT-7_9_3` respecto al proyecto CMake principal. La receta utiliza las rutas de cabeceras y bibliotecas de `find_package(OpenCASCADE 7.9.3 EXACT REQUIRED)` y el runtime OCCT de MSYS2. Compila la biblioteca compartida `m2s_occt_topalgo` y coloca la salida como `libTKTopAlgo.dll` junto a las demás DLL del runtime.

The compiler options are / Las opciones de compilación son: `-fno-devirtualize -fno-devirtualize-speculatively -fno-ipa-icf -fno-lto`. Mesh2Solid's application source is not included in this directory.

No development files from this directory are needed to run Mesh2Solid. / No necesitas estos archivos de desarrollo para ejecutar Mesh2Solid.
