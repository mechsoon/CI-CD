cmake_minimum_required(VERSION 3.16)

project(Canprocess VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.4 REQUIRED COMPONENTS Quick DBus)

qt_standard_project_setup(REQUIRES 6.4)

qt_add_executable(appCanprocess
    test_for_IC2/main.cpp   # main.cpp 경로 수정
)

qt_add_qml_module(appCanprocess
    URI Canprocess
    VERSION 1.0
    QML_FILES
        test_for_IC2/Main.qml      # QML 파일 경로 수정
    SOURCES
        test_for_IC2/SpeedController2.h  # 소스 파일 경로 수정
        test_for_IC2/SpeedController2.cpp
    QML_FILES 
        test_for_IC2/Cluster.qml   # QML 파일 경로 수정
    RESOURCES
        test_for_IC2/resources.qrc # 리소스 파일 경로 수정
)

qt_add_resources(appCanprocess "resources"
    PREFIX "/"
    FILES
        test_for_IC2/Main.qml          # 리소스 경로 수정
        test_for_IC2/Cluster.qml
        test_for_IC2/framefffinal.png
        test_for_IC2/needle.png
        test_for_IC2/needle_battery.png
)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(appCanprocess PROPERTIES
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appCanprocess
    PRIVATE Qt6::Quick Qt6::DBus
)
include_directories(test_for_IC2)
include(GNUInstallDirs)
install(TARGETS appCanprocess
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
