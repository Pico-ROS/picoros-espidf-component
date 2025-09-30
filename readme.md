# Picoros ESP-IDF component
Use for quick integration into ESP-IDF projects.

## Setup

1. Inside ESP-IDF project root:
```sh
# Pull this repository
git clone https://github.com/Pico-ROS/picoros-espidf-component components/picoros
# git clone https://github.com/fish1sheep/picoros-espidf-component.git components/picoros
cd components/picoros && git submodule update --init --recursive
# Copy example ROS types:
cp components/picoros/picoros/examples/example_types.h main/my_ros_types.h
```

2. Add to your main/CMakeLists.txt
```cmake
idf_build_set_property(COMPILE_OPTIONS -DUSER_TYPE_FILE="my_ros_types.h" APPEND)
idf_build_set_property(COMPILE_OPTIONS -I${CMAKE_CURRENT_SOURCE_DIR} APPEND)
```

