# Test plugin; see src/CMakeLists.txt.
ExternalProject_Add(dummy_mtr_fail
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src
  INSTALL_COMMAND ""
  CMAKE_ARGS ${CMAKE_ARGS}
)
