add_definitions(
    -std=gnu99
    -msse2
)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC -Wall -Wno-unused-parameter -Wno-unused-function -O4 -fno-strict-overflow")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

file(GLOB c_files *.c common/*.c)
file(GLOB h_files *.h)
file(GLOB h_files_common common/*.h)

add_library(apriltag SHARED ${c_files})

# Set the library API version. Increment every time the public API changes
set_target_properties(apriltag PROPERTIES SOVERSION 1)

pods_install_headers(${h_files} DESTINATION apriltag)
pods_install_headers(${h_files_common} DESTINATION apriltag/common)

pods_install_libraries(apriltag)

pods_install_pkg_config_file(apriltag
   LIBS -lapriltag
   REQUIRES
   VERSION 0.0.1)

pods_install_libraries(apriltag)
