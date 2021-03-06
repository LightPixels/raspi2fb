cmake_minimum_required(VERSION 2.6)
project(raspi2fb)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")

find_package(PkgConfig)
pkg_check_modules(EGL egl)
pkg_check_modules(LIBBSD libbsd)

include_directories(${EGL_INCLUDE_DIRS} ${LIBBSD_INCLUDE_DIRS})
link_directories(${EGL_LIBRARY_DIRS} ${LIBBSD_LIBRARY_DIRS})

add_executable(${PROJECT_NAME} raspi2fb.c syslogUtilities.c)

target_link_libraries(${PROJECT_NAME} ${EGL_LIBRARIES} ${LIBBSD_LIBRARIES})

set_property(TARGET ${PROJECT_NAME} PROPERTY SKIP_BUILD_RPATH TRUE)
install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
