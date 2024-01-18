
cmake_minimum_required(VERSION 3.0)

#Variables to confige your own specifc project
set(NAME your_project_name)
set(SRC_FILES "${CMAKE_CURRENT_LIST_DIR}/src/*.cpp" ) #Change to fit your project
set(INCLUDE_FILES "${CMAKE_CURRENT_LIST_DIR}/include" ) #Change to fit your project



project(${NAME})

# Adding Raylib Build Config
include(FetchContent)
set(FETCHCONTENT_QUIET FALSE)
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE) # don't build the supplied examples
set(BUILD_GAMES    OFF CACHE BOOL "" FORCE) # don't build the supplied example games


# Where to get Raylib
set(RAYLIB_VERSION 5.0)
FetchContent_Declare(
    raylib
    URL https://github.com/raysan5/raylib/archive/refs/tags/${RAYLIB_VERSION}.tar.gz
    FIND_PACKAGE_ARGS ${RAYLIB_VERSION} EXACT
)

# Get raylib from url
FetchContent_MakeAvailable(raylib)

# LSP
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Adding our source files
file(GLOB_RECURSE PROJECT_SOURCES CONFIGURE_DEPENDS "${SRC_FILES}")
set(PROJECT_INCLUDE "${INCLUDE_FILES}") # Define PROJECT_INCLUDE to be the path to the include directory 

# Setup project
add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_INCLUDE})
target_link_libraries(${PROJECT_NAME} raylib)
