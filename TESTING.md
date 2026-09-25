# Test plugins

Dummy plugins for testing Foundry's CI. They need nothing from MariaDB. Each
installs a README and, where noted, one MTR suite (`SELECT 1`) named after
the plugin.

| Plugin | rpm / deb | bintar | MTR suite |
| --- | --- | --- | --- |
| `dummy_pkg_mtr` | built | built | passes |
| `dummy_pkg` | built | built | none |
| `dummy_bintar_mtr` | fails to build | built | passes |
| `dummy_bintar` | builds, but makes no package | built | none |
| `dummy_uninstallable` | built, won't install (missing dependency) | built | passes, where installed |
| `dummy_mtr_fail` | built | built | fails |

## Expected results

With all of them built:

- rpm/deb builders: the build step warns (2 of 6 failed, at the build and
  package stages), the install step warns (`dummy_uninstallable`), MTR runs
  `dummy_pkg_mtr` and `dummy_mtr_fail` and fails, saving its logs.
- bintar builders: all 6 build, MTR runs the 4 suites and fails on
  `dummy_mtr_fail`.

The suite step's log names every plugin without a suite.

## Testing a subset

A pull request builds only the plugins it changes, so touch the ones you want,
e.g. a line in their README:

| Plugins | Shows |
| --- | --- |
| `dummy_pkg_mtr`, `dummy_pkg` | an all-green run with a suite and a plugin without one |
| `dummy_pkg`, `dummy_bintar` | no suites at all: the test steps are skipped |
| `dummy_pkg_mtr`, `dummy_bintar_mtr` | one plugin failing on rpm/deb, both passing on bintar |
| `dummy_pkg_mtr`, `dummy_uninstallable` | a failed install, with its suite left out |
| `dummy_mtr_fail` | an MTR failure and its saved logs |
