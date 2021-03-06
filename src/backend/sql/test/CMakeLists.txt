
SET(BACKEND_SQL_TEST_INCLUDE_DIRS
  ${CMAKE_BINARY_DIR}/src # for config.h
  ${CMAKE_SOURCE_DIR}/src/backend/sql
  ${CMAKE_SOURCE_DIR}/src/libqof/qof # for qof.
  ${CMAKE_SOURCE_DIR}/src/engine
  ${CMAKE_SOURCE_DIR}/src/test-core
  ${GLIB2_INCLUDE_DIRS}
)

SET(test_backend_sql_SOURCES test-sqlbe.cpp utest-gnc-backend-sql.cpp)

SET(BACKEND_SQL_TEST_LIBS gnc-backend-sql gncmod-engine gnc-qof test-core)

SET_DIST_LIST(test_backend_sql_DIST ${test_backend_sql_SOURCES} CMakeLists.txt
  Makefile.am test-column-types.cpp)

# This test does not actually do anything.
GNC_ADD_TEST(test-column-types test-column-types.cpp
   BACKEND_SQL_TEST_INCLUDE_DIRS BACKEND_SQL_TEST_LIBS
)

GNC_ADD_TEST(test-sqlbe "${test_backend_sql_SOURCES}"
   BACKEND_SQL_TEST_INCLUDE_DIRS BACKEND_SQL_TEST_LIBS
)
TARGET_COMPILE_DEFINITIONS(test-sqlbe PRIVATE TESTPROG=test_sqlbe)