cmake_minimum_required(VERSION 2.8.3)

project(bpcg)

include_directories(include)

find_package(catkin REQUIRED)
find_package(Eigen REQUIRED)

find_package(Boost REQUIRED COMPONENTS thread)
include_directories(include ${Boost_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})

add_definitions(-Wall)

find_package(Eigen)
include_directories(${EIGEN_INCLUDE_DIRS})
add_definitions(${EIGEN_DEFINITIONS})

catkin_package(
    LIBRARIES bpcg
    INCLUDE_DIRS include
    DEPENDS eigen
)

add_library(bpcg
    src/bpcg.cpp
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")

install(TARGETS bpcg DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})

# various compile flags.  -O3 doesn't seem to help; -DNDEBUG seemst to hurt(???)
#rosbuild_add_compile_flags(bpcg -O3 -DNDEBUG -Wno-missing-field-initializers -msse3)
#rosbuild_add_compile_flags(bpcg -g -O0 -DDEBUG=1 -Wno-missing-field-initializers -msse3)
#rosbuild_add_compile_flags(bpcg -O3 -DNDEBUG -Wno-missing-field-initializers )
