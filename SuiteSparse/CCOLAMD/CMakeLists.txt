PROJECT(CCOLAMD)

include_directories("${CCOLAMD_SOURCE_DIR}/Include")

FILE(GLOB LIBHDRS "Include/*.h")
FILE(GLOB LIBSRCS "SourceWrappers/*.c")

ADD_LIBRARY(CCOLAMD ${LIBHDRS} ${LIBSRCS})
ADD_DEPENDENCIES(CCOLAMD SuiteSparse_config)

