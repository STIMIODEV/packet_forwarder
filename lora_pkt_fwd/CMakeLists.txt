find_package(Threads REQUIRED)

include(GNUInstallDirs)

file(READ ${CMAKE_CURRENT_SOURCE_DIR}/../VERSION VERSION)
STRING(REGEX REPLACE "\n" "" VERSION ${VERSION})

add_executable(lora_pkt_fwd
    src/base64.c
    src/jitqueue.c
    src/lora_pkt_fwd.c
    src/parson.c
    src/timersync.c)
target_compile_definitions(lora_pkt_fwd
    PRIVATE VERSION_STRING="${VERSION}")
target_include_directories(lora_pkt_fwd
    PRIVATE inc)
target_link_libraries(lora_pkt_fwd
    PRIVATE loragw Threads::Threads)

install(TARGETS lora_pkt_fwd
        DESTINATION bin)

install(FILES cfg/global_conf.json.PCB_E336.EU868.basic
        DESTINATION ${CMAKE_INSTALL_SYSCONFDIR}/lora
        RENAME global_conf.json)

install(FILES local_conf.json
        DESTINATION ${CMAKE_INSTALL_SYSCONFDIR}/lora)
