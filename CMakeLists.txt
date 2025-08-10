# Get sources
file(GLOB_RECURSE SOURCES_GLOB
        "picoros/thirdparty/Micro-CDR/src/c/*.c"
        "picoros/thirdparty/Micro-CDR/src/c/types*.c"
        "picoros/thirdparty/zenoh-pico/src/api/*.c"
        "picoros/thirdparty/zenoh-pico/src/collections/*.c"
        "picoros/thirdparty/zenoh-pico/src/link/*.c"
        "picoros/thirdparty/zenoh-pico/src/net/*.c"
        "picoros/thirdparty/zenoh-pico/src/protocol/*.c"
        "picoros/thirdparty/zenoh-pico/src/session/*.c"
        "picoros/thirdparty/zenoh-pico/src/transport/*.c"
        "picoros/thirdparty/zenoh-pico/src/utils/*.c"
        "picoros/thirdparty/zenoh-pico/src/system/espidf/*.c"
        "picoros/thirdparty/zenoh-pico/src/system/common/*.c"
        "picoros/src/*.c"
)

# Include directories
set(INCLUDES
        "config"
        "picoros/src/"
        "picoros/thirdparty/Micro-CDR/include/"
        "picoros/thirdparty/zenoh-pico/include/"
        "picoros/thirdparty/zenoh-pico/include/zenoh-pico/"
)

# Register component
idf_component_register(
            SRCS
                ${SOURCES_GLOB}
            INCLUDE_DIRS
                ${INCLUDES}
            REQUIRES
                driver
            )

# Set compile flags
idf_build_set_property(COMPILE_OPTIONS "-DZENOH_ESPIDF" APPEND)
