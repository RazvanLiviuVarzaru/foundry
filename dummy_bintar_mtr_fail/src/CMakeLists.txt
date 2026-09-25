# Test plugin: makes a bintar holding one MTR suite whose test always fails,
# so the run saves its MTR logs. Asked for an rpm or deb, it fails to
# configure, which Foundry reports as a build failure.
# Needs nothing from MariaDB.
cmake_minimum_required(VERSION 3.12)
project(dummy_bintar_mtr_fail LANGUAGES NONE)

if(RPM OR DEB)
  message(FATAL_ERROR "dummy_bintar_mtr_fail only builds bintars")
endif()

install(FILES README DESTINATION share/doc/foundry-dummy-bintar-mtr-fail)
install(DIRECTORY mysql-test/ DESTINATION mariadb-test/plugin/dummy_bintar_mtr_fail)

set(CPACK_GENERATOR TGZ)
set(CPACK_PACKAGE_NAME foundry-dummy-bintar-mtr-fail)
set(CPACK_PACKAGE_VERSION 1.0)
include(CPack)
