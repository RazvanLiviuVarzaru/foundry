ExternalProject_Add(tidesdb
  GIT_REPOSITORY https://github.com/tidesdb/tidesql
  GIT_TAG 4c314c32bd049a9a5c2ff84d5d8a1e61f88d5173
  INSTALL_COMMAND ""
  CMAKE_ARGS ${CMAKE_ARGS}
)
