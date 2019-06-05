add_executable(nx_kit_ut
    src/utils_ut.cpp
    src/output_redirector_ut.cpp
    src/debug_ut.cpp
    src/test_ut.cpp
    src/ini_config_ut.cpp
    src/ini.h
    src/ini.cpp
    src/ini_config_c_usage.h
    src/ini_config_c_usage.c
    src/ini_config_c_ut.cpp
    src/main.cpp
)

IF (MSVC)
    # Setup proper definition of NX_KIT_API for MSVC to link with DLL
    target_compile_definitions(nx_kit_ut PRIVATE NX_KIT_API=__declspec\(dllimport\))
ENDIF()

target_link_libraries(nx_kit_ut nx_kit)

add_test(NAME nx_kit_ut COMMAND nx_kit_ut)
