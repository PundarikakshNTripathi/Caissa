cmake_minimum_required(VERSION 3.10)
project(Caissa VERSION 1.0 LANGUAGES C)

# Modern C99 standard
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Nic Barker's Compiler Flags: Max warnings, Treat warnings as errors, Max Optimization
set(COMMON_FLAGS "-Wall -Wextra -Werror -O3 -march=native -flto")

# Address Sanitizer (ASAN) for catching memory corruption during development
# Note: Remove -fsanitize=address when compiling the final release build for max speed
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${COMMON_FLAGS} -fsanitize=address -g")

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

# 2. Build the Automated Perft Testing Suite
add_executable(caissa_perft tests/perft_suite.c ${ENGINE_SOURCES})

# 3. Build the Texel Tuner Executable
add_executable(caissa_texel tools/texel_tuner.c ${ENGINE_SOURCES})

# 4. Build the SPSA Tuner Executable
add_executable(caissa_spsa tools/spsa_tuner.c ${ENGINE_SOURCES})