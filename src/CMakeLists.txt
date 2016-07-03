cmake_minimum_required(VERSION 2.8)

MESSAGE("Building Annotation Tool for ${SYSTEM_NAME}")
MESSAGE(STATUS "CMAKE_TOOLCHAIN_FILE='${CMAKE_TOOLCHAIN_FILE}'")
MESSAGE(STATUS "CMAKE_SOURCE_DIR='${CMAKE_SOURCE_DIR}'")

# find_package( OpenCV REQUIRED )
# find_package( Boost COMPONENTS system filesystem REQUIRED)
# CMAKE_POLICY(SET CMP0015 NEW)

link_directories(/usr/local/lib)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

include_directories(../include)

file(GLOB C_FILE
    "../lib/*.cc"
)

file(GLOB SRC_LIST
    "../src/*.cpp"
)
file(GLOB ALL_LIB
	opencv_core
	opencv_features2d
	opencv_highgui
	opencv_imgproc
	opencv_video
	opencv_objdetect
	boost_filesystem
	)

# add_library(shared_lib SHARED ${C_FILE})

foreach (SRC ${SRC_LIST})
    get_filename_component(filename ${SRC} NAME_WE) 
    set(TARGET "${filename}.bin")
    message(${TARGET})
    project(${TARGET})
    add_executable(${TARGET} ${SRC} ${C_FILE})
    target_link_libraries( ${TARGET} ${ALL_LIB})
endforeach(SRC ${SRC_LIST})

# ADD_LIBRARY(${PROJ_NAME} SHARED ${GoProLibImganalysis_SRC})
# set(ALL_LIB "${OpenCV_LIBS} ${Boost_FILESYSTEM_LIBRARY} ${Boost_SYSTEM_LIBRARY}")
# set(ALL_LIB "${OpenCV_LIBS}")
# 
# foreach (SRC ${SRC_LIST})
#     get_filename_component(filename ${SRC} NAME_WE) 
#     set(TARGET "${filename}.bin")
#     message(${TARGET})
#     project(${TARGET})
#     add_executable(${TARGET} ${SRC} ${C_FILE})
#     target_link_libraries( ${TARGET} ${ALL_LIB})
# 	INSTALL(TARGETS ${TARGET}
#         	DESTINATION lib)
# endforeach(SRC ${SRC_LIST})
# 
