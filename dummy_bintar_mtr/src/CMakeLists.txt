# Test plugin: makes a bintar holding one passing MTR suite. Asked for an rpm
# or deb, it fails to configure, which Foundry reports as a build failure.
# Needs nothing from MariaDB.
cmake_minimum_required(VERSION 3.12)
project(dummy_bintar_mtr LANGUAGES NONE)

if(RPM OR DEB)
  message(FATAL_ERROR "dummy_bintar_mtr only builds bintars")
endif()

install(FILES README DESTINATION share/doc/foundry-dummy-bintar-mtr)
install(DIRECTORY mysql-test/ DESTINATION mariadb-test/plugin/dummy_bintar_mtr)

set(CPACK_GENERATOR TGZ)
set(CPACK_PACKAGE_NAME foundry-dummy-bintar-mtr)
set(CPACK_PACKAGE_VERSION 1.0)
include(CPack)
