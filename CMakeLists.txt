cmake_minimum_required(VERSION 3.0)

project(lib_RN VERSION 1.0)

include(GNUInstallDirs)

add_library(lib_RN SHARED 
    ReseauNeuronal.cpp 
    Activation.cpp 
    VisualisationReseauNeuronal.cpp 
)

set_target_properties(lib_RN PROPERTIES VERSION ${PROJECT_VERSION})

set_target_properties(lib_RN PROPERTIES PUBLIC_HEADER 
    ReseauNeuronal.h
    Activation.h 
    VisualisationReseauNeuronal.h 
)
configure_file(lib_RN.pc.in lib_RN.pc @ONLY)

find_package(Armadillo REQUIRED)
include_directories(${ARMADILLO_INCLUDE_DIRS})

find_package(SFML COMPONENTS graphics window system REQUIRED)

# add_library(lib_RN ${SRCS} ${HEADERS})

target_link_libraries(lib_RN sfml-graphics sfml-window sfml-system)
target_link_libraries(lib_RN ${ARMADILLO_LIBRARIES})

install(TARGETS lib_RN
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# install(TARGETS lib_RN
#     LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
# install(TARGETS lib_RN PUBLIC_HEADERS DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(FILES ${CMAKE_BINARY_DIR}/lib_RN.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)

# set(SRCS
    # ReseauNeuronal.cpp
    # Activation.cpp
    # VisualisationReseauNeuronal.cpp
# )

# set(HEADERS 
    # ReseauNeuronal.h
    # Activation.h
    # VisualisationReseauNeuronal.h
# )

