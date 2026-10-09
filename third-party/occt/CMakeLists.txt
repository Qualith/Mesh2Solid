# OCCT 7.9.3 source is prepared and hash-checked by scripts/prepare-occt-source.ps1.
# Only TKTopAlgo is rebuilt; all other modules use the pinned MSYS2 runtime.
set(_source "${CMAKE_SOURCE_DIR}/.tools/OCCT-7_9_3")
if(NOT EXISTS "${_source}/src/TKTopAlgo/PACKAGES")
  message(FATAL_ERROR "Run scripts/prepare-occt-source.ps1 before configuring: OCCT classifier source is missing")
endif()
file(STRINGS "${_source}/src/TKTopAlgo/PACKAGES" _packages)
set(_files)
set(_includes)
foreach(_package IN LISTS _packages)
  list(APPEND _includes "${_source}/src/${_package}")
  file(STRINGS "${_source}/src/${_package}/FILES" _entries)
  foreach(_entry IN LISTS _entries)
    if(_entry MATCHES "\\.(cxx|cpp|c)$")
      list(APPEND _files "${_source}/src/${_package}/${_entry}")
    endif()
  endforeach()
endforeach()
add_library(m2s_occt_topalgo SHARED ${_files})
set_target_properties(m2s_occt_topalgo PROPERTIES OUTPUT_NAME TKTopAlgo
  AUTOMOC OFF CXX_STANDARD 17 CXX_STANDARD_REQUIRED ON
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/runtime")
target_include_directories(m2s_occt_topalgo PRIVATE ${_includes} ${OpenCASCADE_INCLUDE_DIR})
# Prevent the vendor selector miscompilation observed in BRepClass3d.
target_compile_options(m2s_occt_topalgo PRIVATE -fno-devirtualize
  -fno-devirtualize-speculatively -fno-ipa-icf -fno-lto)
target_link_options(m2s_occt_topalgo PRIVATE -fno-lto -Wl,--export-all-symbols)
foreach(_dependency TKMath TKernel TKG2d TKG3d TKGeomBase TKBRep TKGeomAlgo)
  target_link_libraries(m2s_occt_topalgo PRIVATE "${OpenCASCADE_LIBRARY_DIR}/lib${_dependency}.dll.a")
endforeach()
add_custom_command(TARGET m2s_occt_topalgo POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_if_different "$<TARGET_FILE:m2s_occt_topalgo>" "${CMAKE_BINARY_DIR}/libTKTopAlgo.dll")
