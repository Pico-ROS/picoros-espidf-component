# Picoros ESP-IDF component
Builds [Pico-ROS](https://github.com/Pico-ROS/Pico-ROS-software), Micro-CDR and zenoh-pico from the `picoros`
submodule as one ESP-IDF component named `picoros`. Nothing is copied: zenoh-pico's `config.h` is generated at
configure time from the checked-out submodule and the feature flags below.

## Setup

1. Inside your ESP-IDF project root, as a clone or a submodule:
```sh
git clone https://github.com/Pico-ROS/picoros-espidf-component components/picoros
git -C components/picoros submodule update --init --recursive
```
ESP-IDF names a component after its directory, so keep `components/picoros`. If the checkout has to live
elsewhere, a one-line `components/picoros/CMakeLists.txt` that `include()`s this repository's `CMakeLists.txt`
does the same job (see [examples/esp32p4_nano/components/picoros](examples/esp32p4_nano/components/picoros/CMakeLists.txt)).

2. Add `REQUIRES picoros` to the components that use it and include `picoros.h` / `picoserdes.h`.

3. Optional, in the project `CMakeLists.txt` before `include($ENV{IDF_PATH}/tools/cmake/project.cmake)`:
```cmake
set(PICOROS_USER_TYPE_FILE "my_ros_types.h")                           # your ROS types header, see picoros/src/picoserdes.h
set(PICOROS_USER_TYPE_INCLUDE_DIRS "${CMAKE_CURRENT_LIST_DIR}/main")   # where that header lives (absolute paths)
set(PICOROS_ZENOH_CMAKE_ARGS -DZ_FEATURE_MULTI_THREAD=1 -DZ_FEATURE_LINK_TCP=1 ... -DZ_TRANSPORT_LEASE=60000)
set(PICOROS_ZENOH_LOG INFO)                                            # zenoh-pico log level: ERROR, WARN, INFO, DEBUG, TRACE
set(PICOROS_DEBUG ON)                                                  # Pico-ROS logging
```

| Variable | Default |
|---|---|
| `PICOROS_USER_TYPE_FILE` | `example_types.h` |
| `PICOROS_USER_TYPE_INCLUDE_DIRS` | `picoros/examples` (where `example_types.h` lives) |
| `PICOROS_ZENOH_CMAKE_ARGS` | TCP client only, no scouting/multicast/serial, `Z_TRANSPORT_LEASE=60000`, `Z_TRANSPORT_LEASE_EXPIRE_FACTOR=2` (matches `rmw_zenohd` defaults) |
| `PICOROS_DEBUG` | `OFF` |
| `PICOROS_ZENOH_LOG` | off |

Any zenoh-pico `Z_FEATURE_*` / `Z_*` CMake option can be passed in `PICOROS_ZENOH_CMAKE_ARGS`; the list replaces
the default, so repeat the flags you want to keep. `picoparams` is not part of the component.

## Example

[examples/esp32p4_nano](examples/esp32p4_nano/) is a complete project for the Waveshare ESP32-P4-NANO (Ethernet):
talker/listener against `rmw_zenohd`.
