cmake_minimum_required(VERSION 2.6)
PROJECT(SQLite)

###########################################
# Source files for SQLite
SET( SQLITE_SRCS
  sqlite3.h
  sqlite3ext.h
  sqlite3.c
)

ADD_DEFINITIONS(-DSQLITE_ENABLE_COLUMN_METADATA)

###########################################
# Set the name of the library
SET(SCI_SQLITE_LIBRARY sqlite CACHE INTERNAL "SQLite Library name." FORCE)

###########################################
# Include directory of SQLite
SET(SCI_SQLITE_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR} CACHE INTERNAL "SQLite include directories" FORCE)

ADD_LIBRARY(${SCI_SQLITE_LIBRARY} SHARED ${SQLITE_SRCS})

SET(SCI_SQLITE_LIBRARY_DIR ${CMAKE_CURRENT_BINARY_DIR})
SET(SQLITE_USE_FILE "${CMAKE_CURRENT_SOURCE_DIR}/UseSQLite.cmake")

CONFIGURE_FILE(SQLiteConfig.cmake.in "${CMAKE_CURRENT_BINARY_DIR}/SQLiteConfig.cmake" @ONLY)
EXPORT(TARGETS ${SCI_SQLITE_LIBRARY} FILE SQLiteExports.cmake)
