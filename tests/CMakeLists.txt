if (XCB_ICCCM_FOUND)
    set(normalhintsbasesizetest_SRCS normalhintsbasesizetest.cpp)
    add_executable(normalhintsbasesizetest ${normalhintsbasesizetest_SRCS})
    target_link_libraries(normalhintsbasesizetest XCB::XCB XCB::ICCCM KF5::WindowSystem)
endif()

# next target
set(screenedgeshowtest_SRCS screenedgeshowtest.cpp)
add_executable(screenedgeshowtest ${screenedgeshowtest_SRCS})
target_link_libraries(screenedgeshowtest Qt5::Widgets Qt5::X11Extras KF5::ConfigCore KF5::WindowSystem KF5::WaylandClient ${XCB_XCB_LIBRARY})

if (KF5Wayland_FOUND)
    add_definitions(-DSOURCE_DIR="${KWIN_SOURCE_DIR}")
    set(waylandclienttest_SRCS
            waylandclienttest.cpp
       )
    add_executable(waylandclienttest ${waylandclienttest_SRCS})
    target_link_libraries(waylandclienttest Qt5::Core Qt5::Gui KF5::WaylandClient)
endif()

if (HAVE_INPUT)
    set(libinputtest_SRCS
            libinputtest.cpp
            ${KWIN_SOURCE_DIR}/libinput/context.cpp
            ${KWIN_SOURCE_DIR}/libinput/connection.cpp
            ${KWIN_SOURCE_DIR}/libinput/device.cpp
            ${KWIN_SOURCE_DIR}/libinput/events.cpp
            ${KWIN_SOURCE_DIR}/libinput/libinput_logging.cpp
            ${KWIN_SOURCE_DIR}/logind.cpp
            ${KWIN_SOURCE_DIR}/udev.cpp
    )
    add_executable(libinputtest ${libinputtest_SRCS})
    add_definitions(-DKWIN_BUILD_TESTING)
    target_link_libraries(libinputtest Qt5::Core Qt5::DBus Libinput::Libinput ${UDEV_LIBS} KF5::ConfigCore KF5::GlobalAccel KF5::WindowSystem)
endif()

add_executable(x11shadowreader x11shadowreader.cpp)
target_link_libraries(x11shadowreader XCB::XCB Qt5::Widgets Qt5::X11Extras KF5::ConfigCore KF5::WindowSystem)
