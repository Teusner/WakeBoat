cmake_minimum_required(VERSION 3.20)
project(WakeBoat)

# Settings
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O3 -lpthread -std=c++17")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3 -lpthread -std=c++17")

################################################################################
# Looking for IBEX
################################################################################
find_package(IBEX REQUIRED)
ibex_init_common() # IBEX should have installed this function
message(STATUS "Found IBEX version ${IBEX_VERSION}")

################################################################################
# Looking for CODAC
################################################################################
find_package(CODAC REQUIRED)
message(STATUS "Found Codac version ${CODAC_VERSION}")
include_directories(${CODAC_INCLUDE_DIRS})
message(STATUS "Codac Include dirs ${CODAC_INCLUDE_DIRS}")

################################################################################
# Looking for IPE-Generator
################################################################################
find_package(ipegenerator REQUIRED)
message(STATUS "Found ipegenerator")
include_directories(${IPEGENERATOR_INCLUDE_DIRS})
set(LIBS ${IPEGENERATOR_LIBRARIES} ${LIBS})

################################################################################
# Looking for Eigen
################################################################################
find_package(Eigen3 REQUIRED NO_MODULE)
include_directories(${EIGEN3_INCLUDE_DIRS})

################################################################################
# Looking for FMT
################################################################################
find_package(fmt REQUIRED)
message(STATUS "Found FMT version ${FMT_VERSION}")
include_directories(${fmt_INCLUDE_DIRS})

################################################################################
# Looking for CXXOPTS
################################################################################
add_subdirectory(extern/cxxopts)

################################################################################
# Looking for ryml
################################################################################
find_package(ryml REQUIRED)

################################################################################
# Looking for Poisson-Disk-Generator
################################################################################
include_directories(extern/poisson-disk-generator)

################################################################################
# Looking for THREADS
################################################################################
find_package (Threads)

################################################################################
# Compile sources
################################################################################
add_library(wake_boat src/scene.cpp src/utils.cpp)
target_include_directories(wake_boat PUBLIC ${fmt_INCLUDE_DIRS})
target_link_libraries(wake_boat ${CODAC_LIBRARIES} Ibex::ibex ${IPEGENERATOR_LIBRARIES} fmt::fmt)

add_executable(main src/main.cpp)
target_include_directories(main PUBLIC cxxopts)
target_link_libraries(main ${CODAC_LIBRARIES} Ibex::ibex ${IPEGENERATOR_LIBRARIES} fmt::fmt cxxopts ${CMAKE_THREAD_LIBS_INIT} wake_boat ryml::ryml)

# add_subdirectory(test)