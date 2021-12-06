cmake_minimum_required(VERSION 3.18)

message(STATUS "Downloading vcpkg")
include("FetchContent")

set(VCPKG_TARGET_TRIPLET x64-windows-static)

FetchContent_Declare(vcpkg GIT_REPOSITORY https://github.com/Microsoft/vcpkg.git SOURCE_SUBDIR vcpkg)
FetchContent_MakeAvailable(vcpkg)

set(CMAKE_TOOLCHAIN_FILE "${vcpkg_SOURCE_DIR}/scripts/buildsystems/vcpkg.cmake")

project(vcpkg-wxwidgets)


find_package(wxWidgets REQUIRED)
message(${wxWidgets_LIBRARIES})

add_executable(App WIN32 main.cpp)

# set_property(TARGET App PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
set_property(TARGET App PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded")

target_link_libraries(App ${wxWidgets_LIBRARIES})
target_include_directories(App PRIVATE ${wxWidgets_INCLUDE_DIRS})
