cmake_minimum_required(VERSION 3.24)
project(Munchies LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# --- SDL3 -------------------------------------------------------------------
# Downloaded and built from source automatically on first configure, so nobody
# needs to install SDL3 by hand. Pinned to one version so everyone matches.
# Uses a system-installed SDL3 only if you pass -DMUNCHIES_USE_SYSTEM_SDL3=ON.
include(FetchContent)
option(MUNCHIES_USE_SYSTEM_SDL3 "Prefer a system-installed SDL3" OFF)

set(SDL_SHARED OFF CACHE BOOL "" FORCE)   # link statically: nothing to ship
set(SDL_STATIC ON  CACHE BOOL "" FORCE)
set(SDL_TEST_LIBRARY OFF CACHE BOOL "" FORCE)

if(MUNCHIES_USE_SYSTEM_SDL3)
  set(_sdl_find FIND_PACKAGE_ARGS 3.2 CONFIG)
else()
  set(_sdl_find "")
endif()

FetchContent_Declare(
  SDL3
  GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
  GIT_TAG        release-3.4.20
  GIT_SHALLOW    TRUE
  ${_sdl_find}
)
FetchContent_MakeAvailable(SDL3)

# --- App --------------------------------------------------------------------
add_executable(Munchies src/main.cpp)
target_link_libraries(Munchies PRIVATE SDL3::SDL3)
