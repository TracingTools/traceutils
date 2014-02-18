project(traceutils CXX)
cmake_minimum_required(VERSION 2.6.2)

set(CMAKE_SUPPRESS_REGENERATION TRUE)

# Find the location of libtrace library.
find_path(LIBTRACE_FOLDER NAMES libtrace/CMakeLists.txt
          HINTS . .. third_party)
if (LIBTRACE_FOLDER)
 set(LIBTRACE_ROOT ${LIBTRACE_FOLDER}/libtrace)
endif (LIBTRACE_FOLDER)

add_subdirectory(${LIBTRACE_ROOT} libtrace)

include_directories(${LIBTRACE_ROOT}/src)

add_executable(tracedump tracedump/tracedump.cc)
target_link_libraries(tracedump
    base
    event
    parser
    )