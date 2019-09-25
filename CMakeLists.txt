cmake_minimum_required(VERSION 3.7.0)
project(stduuid CXX)

add_library(libuuid INTERFACE)
target_compile_definitions(libuuid INTERFACE NO_SYSTEM_UUID)
target_include_directories(libuuid INTERFACE 
  $<BUILD_INTERFACE:${stduuid_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
  )

file(GLOB_RECURSE includes include/gsl/*)
install(FILES include/uuid.h TYPE INCLUDE)
install(FILES lib/cmake/libuuid-config.cmake DESTINATION lib/cmake)
install(DIRECTORY include/gsl TYPE INCLUDE)


install(TARGETS libuuid
  EXPORT libuuid-Targets
  )

export(EXPORT libuuid-Targets)

install(EXPORT libuuid-Targets
  DESTINATION lib/cmake
  NAMESPACE libuuid::
  )
