cmake_minimum_required(VERSION 3.7)  # 3.7: CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT, 3.3: CXX_STANDARD
project(Warships CXX)

set(SOURCES src/main.cpp src/gameboard.cpp)

if(CMAKE_CXX_COMPILER_ID STREQUAL GNU)
  list(APPEND FLAGS -Wall)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL Clang)
  list(APPEND FLAGS -Wall)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL Intel)
  list(APPEND FLAGS -w2)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL PGI)
  list(APPEND FLAGS -a)
endif()

add_executable(Warships ${SOURCES})
target_include_directories(Warships PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/headers/)
target_compile_options(Warships PRIVATE ${FLAGS})

set_target_properties(Warships PROPERTIES
  CXX_STANDARD 14
  CXX_STANDARD_REQUIRED true)

# --- install

if(UNIX AND CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "~/.local" CACHE PATH "..." FORCE)
endif()

install(TARGETS Warships
  RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/data
        DESTINATION ${CMAKE_INSTALL_PREFIX})
