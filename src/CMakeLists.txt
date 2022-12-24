file(GLOB SRC_LIST "*.cpp" "*.c")

find_package(PkgConfig)
pkg_search_module(DBUS IMPORTED_TARGET dbus-1)
message(STATUS "found library:${DBUS_LIBRARIES}")

set(SERVER server)
set(CLIENT client)

ADD_EXECUTABLE(${SERVER} server.cpp)

target_link_libraries(${SERVER}
    PRIVATE ${DBUS_LIBRARIES}
)

install(TARGETS ${SERVER} DESTINATION output)

ADD_EXECUTABLE(${CLIENT} client.cpp)

target_link_libraries(${CLIENT}
    PRIVATE ${DBUS_LIBRARIES}
)

install(TARGETS ${CLIENT} DESTINATION output)