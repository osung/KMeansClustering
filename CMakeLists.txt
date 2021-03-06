cmake_minimum_required(VERSION 2.6)

Project(KMeansClustering)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=gnu++0x")

include_directories(/media/portable/src/Eigen)

# Submodules

# Only include EigenHelpers if it is not already available
if(NOT TARGET EigenHelpers)
  add_subdirectory(EigenHelpers)
endif()

if(NOT TARGET Helpers)
 add_subdirectory(Helpers)
endif()

add_library(KMeansClustering KMeansClustering.cpp)
TARGET_LINK_LIBRARIES(KMeansClustering EigenHelpers)

SET(KMeansClustering_BuildExamples OFF CACHE BOOL "KMeansClustering_BuildExamples")
if(KMeansClustering_BuildExamples)
  ADD_EXECUTABLE(KMeansClusteringExample Example.cpp)
  TARGET_LINK_LIBRARIES(KMeansClusteringExample KMeansClustering EigenHelpers)
endif(KMeansClustering_BuildExamples)
