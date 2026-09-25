# Test plugin: makes an rpm, deb or bintar holding two passing MTR suites,
# dummy_suite_a and dummy_suite_b. Needs nothing from MariaDB.
cmake_minimum_required(VERSION 3.12)
project(dummy_two_suites LANGUAGES NONE)

# Foundry passes -DRPM=1 or -DDEB=1; neither means a bintar. MTR suites go
# where MariaDB's rpm, deb and bintar layouts put them.
if(RPM)
  set(CPACK_GENERATOR RPM)
  set(mtr_dir share/mariadb-test)
elseif(DEB)
  set(CPACK_GENERATOR DEB)
  set(mtr_dir share/mariadb/mariadb-test)
else()
  set(CPACK_GENERATOR TGZ)
  set(mtr_dir mariadb-test)
endif()

install(FILES README DESTINATION share/doc/foundry-dummy-two-suites)
install(DIRECTORY mysql-test/ DESTINATION ${mtr_dir}/plugin/dummy_two_suites)

set(CPACK_PACKAGE_NAME foundry-dummy-two-suites)
set(CPACK_PACKAGE_VERSION 1.0)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Foundry test plugin")
set(CPACK_PACKAGE_CONTACT "Foundry CI <foundry@example.invalid>")
set(CPACK_RPM_FILE_NAME RPM-DEFAULT)
set(CPACK_RPM_PACKAGE_ARCHITECTURE noarch)
# Leave MariaDB-test's own directories to it.
set(CPACK_RPM_EXCLUDE_FROM_AUTO_FILELIST_ADDITION
  /usr/share/mariadb-test /usr/share/mariadb-test/plugin)
set(CPACK_DEBIAN_FILE_NAME DEB-DEFAULT)
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE all)
include(CPack)
