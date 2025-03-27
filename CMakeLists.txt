

#[[add_definitions(CONFIG_ZENOH_PICO_LINK_SERIAL)
add_definitions("-DCONFIG_ZENOH_PICO_MULTI_THREAD=0")
add_definitions("-DCONFIG_ZENOH_PICO_PUBLICATION=1")
add_definitions("-DCONFIG_ZENOH_PICO_SUBSCRIPTION=1")
add_definitions("-DCONFIG_ZENOH_PICO_QUERY=0")
add_definitions("-DCONFIG_ZENOH_PICO_QUERYABLE=0")
add_definitions("-DCONFIG_ZENOH_PICO_RAWETH_TRANSPORT=0")
add_definitions("-DCONFIG_ZENOH_PICO_LINK_TCP=0")
add_definitions("-DCONFIG_ZENOH_PICO_LINK_UDP_UNICAST=0")
add_definitions("-DCONFIG_ZENOH_PICO_LINK_UDP_MULTICAST=0")
add_definitions("-DCONFIG_ZENOH_PICO_SCOUTING_UDP=0")
add_definitions("-DCONFIG_ZENOH_PICO_LINK_WS=0")]]

file(GLOB_RECURSE Sources
        "src/api/*.c"
        "src/collections/*.c"
        "src/link/*.c"
        "src/net/*.c"
        "src/protocol/*.c"
        "src/session/*.c"
        "src/transport/*.c"
        "src/utils/*.c"
        "src/system/common/*.c"
)

file (GLOB Sources_Esp "src/system/espidf/*.c")
list(APPEND Sources ${Sources_Esp})

idf_component_register(SRCS "${Sources}" PRIV_REQUIRES driver INCLUDE_DIRS "include")
target_compile_options(${COMPONENT_LIB} PRIVATE -Wno-error=stringop-truncation -Wno-error=maybe-uninitialized)
target_compile_definitions(${COMPONENT_LIB} PRIVATE ZENOH_ESPIDF=1 Z_FEATURE_UNSTABLE_API=1 Z_FEATURE_MATCHING=1)