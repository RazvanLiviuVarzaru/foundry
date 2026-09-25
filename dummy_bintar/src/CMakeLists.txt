# Test plugin: makes a bintar with no MTR suite. Asked for an rpm or deb, it
# builds but makes no package, which Foundry reports as "No packages found".
# Needs nothing from MariaDB.
cmake_minimum_required(VERSION 3.12)
project(dummy_bintar LANGUAGES NONE)

if(RPM OR DEB)
  add_custom_target(package COMMAND ${CMAKE_COMMAND} -E echo "No rpm or deb for dummy_bintar")
  return()
endif()

install(FILES README DESTINATION share/doc/foundry-dummy-bintar)

set(CPACK_GENERATOR TGZ)
set(CPACK_PACKAGE_NAME foundry-dummy-bintar)
set(CPACK_PACKAGE_VERSION 1.0)
include(CPack)
