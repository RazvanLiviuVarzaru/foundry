# Test plugin: makes an rpm, deb or bintar holding one passing MTR
# suite. The rpm and deb need a package nothing provides, so they won't install,
# and their suite must then be left out of the MTR run.
# Needs nothing from MariaDB.
cmake_minimum_required(VERSION 3.12)
project(dummy_uninstallable LANGUAGES NONE)

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

install(FILES README DESTINATION share/doc/foundry-dummy-uninstallable)
install(DIRECTORY mysql-test/ DESTINATION ${mtr_dir}/plugin/dummy_uninstallable)

set(CPACK_PACKAGE_NAME foundry-dummy-uninstallable)
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
# A dependency no repository provides.
set(CPACK_RPM_PACKAGE_REQUIRES foundry-nonexistent-dependency)
set(CPACK_DEBIAN_PACKAGE_DEPENDS foundry-nonexistent-dependency)
include(CPack)
