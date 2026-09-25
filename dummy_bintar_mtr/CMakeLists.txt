# Test plugin; see src/CMakeLists.txt.
ExternalProject_Add(dummy_bintar_mtr
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src
  INSTALL_COMMAND ""
  CMAKE_ARGS ${CMAKE_ARGS}
)
