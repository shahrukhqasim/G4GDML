cmake_minimum_required(VERSION 3.16...3.27)
project(G4GDML)

set(CMAKE_CXX_STANDARD 17)

option(WITH_GEANT4_VIS "Build example with Geant4 Vis drivers" ON)
if(WITH_GEANT4_VIS)
    find_package(Geant4 REQUIRED vis_all)
else()
    find_package(Geant4)
endif()

find_library(XERCES_LIBRARY xerces-c HINTS /opt/homebrew/lib)

include_directories(${PROJECT_SOURCE_DIR}/include
        ${Geant4_INCLUDE_DIR}
        /opt/homebrew/include/)

        # Find all source files in the src directory
file(GLOB G4GDML_SRC_FILES ${PROJECT_SOURCE_DIR}/src/*.cc)

# Find all header files in the include directory
file(GLOB G4GDML_HEADER_FILES ${PROJECT_SOURCE_DIR}/include/*.h)

MESSAGE(${G4GDML_SRC_FILES})

add_library(g4gdml STATIC ${G4GDML_SRC_FILES} ${G4GDML_HEADER_FILES})

target_link_libraries(g4gdml ${Geant4_LIBRARIES}  ${XERCES_LIBRARY})

