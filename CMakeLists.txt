cmake_minimum_required(VERSION 3.13.4)

project(za.S.H.I.T.ka)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

option(FORCE_COLORED_OUTPUT "Always produce ANSI-colored output (GNU/Clang only)." ON)

if(${FORCE_COLORED_OUTPUT})
  message("-- Force colored output enabled")

  if("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
     add_compile_options(-fdiagnostics-color=always)
  elseif("${CMAKE_C_COMPILER_ID}" STREQUAL "Clang")
     add_compile_options(-fcolor-diagnostics)
  endif()
endif()

# TODO: rewrite this line using 'target_include_directories'
include_directories(include)

set(CIPHER_LIST ""  CACHE INTERNAL "")
set(OPT_LEVELS O0 O1 O2 O3 Os CACHE INTERNAL "")
add_subdirectory(lib)
message("-- Registered ciphers: ${CIPHER_LIST}")
add_subdirectory(tools)

enable_testing()
set(BUILD_TESTING ON)
add_subdirectory(test)

