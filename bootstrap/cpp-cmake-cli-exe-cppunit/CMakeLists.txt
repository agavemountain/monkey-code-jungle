cmake_minimum_required(VERSION 2.8.11)
project(hello)

##############################################################################
# Find CppUnit
##############################################################################
INCLUDE(FindPkgConfig)
PKG_CHECK_MODULES(CPPUNIT "cppunit")
IF(NOT CPPUNIT_FOUND)
    FIND_PATH(CPPUNIT_INCLUDE_DIRS cppunit/TestCase.h
      /usr/local/include
      /usr/include
    )

    FIND_LIBRARY(CPPUNIT_LIBRARIES cppunit
               ${CPPUNIT_INCLUDE_DIRS}/../lib
               /usr/local/lib
               /usr/lib)

    IF(CPPUNIT_INCLUDE_DIRS)
      IF(CPPUNIT_LIBRARIES)
        SET(CPPUNIT_FOUND "YES")
        SET(CPPUNIT_LIBRARIES ${CPPUNIT_LIBRARIES} ${CMAKE_DL_LIBS})
      ENDIF(CPPUNIT_LIBRARIES)
    ENDIF(CPPUNIT_INCLUDE_DIRS)

    INCLUDE(FindPackageHandleStandardArgs)
    FIND_PACKAGE_HANDLE_STANDARD_ARGS(CPPUNIT DEFAULT_MSG CPPUNIT_LIBRARIES CPPUNIT_INCLUDE_DIRS)
ENDIF(NOT CPPUNIT_FOUND)

IF(CPPUNIT_FOUND)
    MESSAGE("FOUND cppunit.")
ELSE()
    MESSAGE("CPPUNIT NOT FOUND.")
ENDIF(CPPUNIT_FOUND)


include( CTest )
add_subdirectory( src )
add_subdirectory( unittest )

INCLUDE(CPack)

