cmake_minimum_required(VERSION 3.3.2)

project(nx_kit_test)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)

set(nxKitLibraryType "SHARED" CACHE STRING "nx_kit library type (STATIC or SHARED or empty)")

set(nx_kit_files
    src/nx/kit/utils.h
    src/nx/kit/utils.cpp
    src/nx/kit/debug.h
    src/nx/kit/debug.cpp
    src/nx/kit/ini_config.h
    src/nx/kit/ini_config.cpp
    src/nx/kit/output_redirector.h
    src/nx/kit/output_redirector.cpp
    src/nx/kit/test.h
    src/nx/kit/test.cpp
    src/ini_config_c.h
    src/ini_config_c_impl.h
)

add_library(nx_kit ${nxKitLibraryType} ${nx_kit_files})

target_include_directories(nx_kit PUBLIC src)

# Set the maximum warning level.
IF (MSVC)
    add_compile_definitions(NX_KIT_API=__declspec\(dllexport\))
    add_compile_options(/W4 /WX)
ELSE()
    add_compile_definitions(NX_KIT_API=__attribute__\(\(visibility\(\"default\"\)\)\))
    add_compile_options(-Wall -Wextra -Werror)
ENDIF()

set(nxKitWithTests "YES" CACHE STRING "Whether to build unit tests")
if(nxKitWithTests)
    enable_testing()
    add_subdirectory(unit_tests)
endif()
