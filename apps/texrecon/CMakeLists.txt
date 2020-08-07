file (GLOB HEADERS "*.h")
file (GLOB SOURCES "[^_]*.cpp")

set(BIN texrecon)

add_executable(${BIN} ${SOURCES})
set_property(TARGET ${BIN} PROPERTY INTERPROCEDURAL_OPTIMIZATION True)
add_dependencies(${BIN} ext_mve)
target_link_libraries(${BIN} tex
        TBB::tbb
        TBB::tbbmalloc_proxy
        TBB::tbbmalloc
        -lmve -lmve_util)
target_compile_options(${BIN} PUBLIC -march=native)
install(TARGETS ${BIN} RUNTIME DESTINATION bin)
