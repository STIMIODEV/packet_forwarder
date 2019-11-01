find_package(Threads REQUIRED)

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

