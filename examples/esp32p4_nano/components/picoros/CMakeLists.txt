# ESP-IDF names a component after its directory, so this wrapper gives the repository root the name `picoros`
# without a copy or a symlink. Projects that clone the repository as `components/picoros` don't need it.
include("${CMAKE_CURRENT_LIST_DIR}/../../../../CMakeLists.txt")
