# Test plugin: makes an rpm, deb or bintar with no MTR suite.
# Needs nothing from MariaDB.
cmake_minimum_required(VERSION 3.12)
project(dummy_pkg LANGUAGES NONE)

# Foundry passes -DRPM=1 or -DDEB=1; neither means a bintar.
if(RPM)
  set(CPACK_GENERATOR RPM)
elseif(DEB)
  set(CPACK_GENERATOR DEB)
else()
  set(CPACK_GENERATOR TGZ)
endif()

install(FILES README DESTINATION share/doc/foundry-dummy-pkg)

set(CPACK_PACKAGE_NAME foundry-dummy-pkg)
set(CPACK_PACKAGE_VERSION 1.0)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Foundry test plugin")
set(CPACK_PACKAGE_CONTACT "Foundry CI <foundry@example.invalid>")
set(CPACK_RPM_FILE_NAME RPM-DEFAULT)
set(CPACK_RPM_PACKAGE_ARCHITECTURE noarch)
set(CPACK_DEBIAN_FILE_NAME DEB-DEFAULT)
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE all)
include(CPack)
