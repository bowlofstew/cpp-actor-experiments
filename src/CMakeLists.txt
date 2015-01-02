list( APPEND CMAKE_CXX_FLAGS "-std=c++0x ${CMAKE_CXX_FLAGS} -g -ftest-coverage -fprofile-arcs")
externalproject_add(
  actor-framework
  GIT_REPOSITORY https://github.com/actor-framework/actor-framework.git
  GIT_TAG 14467ae0755be44fa6abc37abcfa4397aa4483d8
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../thirdparty/actor-framework
  CONFIGURE_COMMAND ./configure --prefix=${CMAKE_INSTALL_PREFIX}
  BUILD_COMMAND "make"
  INSTALL_COMMAND ""
  BUILD_IN_SOURCE 1
)
set(ACTOR_INC ${CMAKE_CURRENT_SOURCE_DIR}/../thirdparty/actor-framework/libcaf_core)
include_directories(${ACTOR_INC})
link_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/../thirdparty/actor-framework/build/lib
)
add_executable(actor-play main.cc)
add_dependencies(actor-play actor-framework)
target_link_libraries(actor-play
  libcaf_core.a
)

