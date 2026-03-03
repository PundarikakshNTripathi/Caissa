cmake_minimum_required(VERSION 3.10)
project(Caissa VERSION 1.0 LANGUAGES C)

# Modern C99 standard and maximum performance optimization
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3 -Wall -Wextra -march=native -flto")

include_directories(include)

# Core engine source files
set(ENGINE_SOURCES 
    src/board.c
    src/evaluate.c
    src/magics.c
    src/move_ordering.c
    src/movegen.c
    src/search.c
    src/transposition.c
    src/uci_protocol.c
    src/utils.c
)

# 1. Build the Main Chess Engine Executable
add_executable(caissa src/main.c ${ENGINE_SOURCES})

# 2. Build the Texel Tuner Executable
add_executable(caissa_texel tools/texel_tuner.c ${ENGINE_SOURCES})

# 3. Build the SPSA Tuner Executable
add_executable(caissa_spsa tools/spsa_tuner.c ${ENGINE_SOURCES})