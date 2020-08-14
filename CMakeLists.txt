PROJECT(SuiteSparseProject)
cmake_minimum_required(VERSION 2.6)

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

add_subdirectory(metis)
add_subdirectory(CLAPACK)
add_subdirectory(SuiteSparse)

#add_subdirectory(SPQR)


# Parse config file:
# -------------------------------------------------
SET(THE_SuiteSparse_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/SuiteSparse/")
SET(THE_SuiteSparse_LIBS_INCL_DIR "${CMAKE_CURRENT_SOURCE_DIR}/SuiteSparse/include")
SET(THE_CMAKE_BINARY_DIR "${CMAKE_BINARY_DIR}")
SET(SuiteSparse_LINKER_LIBS "${SuiteSparse_LINKER_LIBS};metis")

IF (UNIX)
	SET(SuiteSparse_LINKER_LIBS
		${SuiteSparse_LINKER_LIBS}
		lapack
		blas
		rt
		)
ELSE(UNIX)
	SET(SuiteSparse_LINKER_LIBS
		${SuiteSparse_LINKER_LIBS}
		blas
		lapack
		)
ENDIF(UNIX)

CONFIGURE_FILE(
	"${CMAKE_CURRENT_SOURCE_DIR}/SuiteSparseConfig.cmake.in"
	"${CMAKE_CURRENT_BINARY_DIR}/SuiteSparseConfig.cmake"
	@ONLY)
	
