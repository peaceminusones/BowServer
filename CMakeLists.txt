set(CMAKE_CXX_COMPILER g++)
set(CMAKE_C_COMPILER gcc)

cmake_minimum_required(VERSION 3.1)
project(BowServer C CXX)
set(CMAKE_CXX_STANDARD 17)

set(BOW_CXXFLAGS "-Wno-write-strings -Wno-pointer-arith")
#-fsanitize=address 
add_definitions("-g") 
#add_definitions("-DSPDLOG_COMPILED_LIB -lspdlog") 

set(CMAKE_CXX_FLAGS ${BOW_CXXFLAGS})
    
if(NOT TARGET spdlog)
    find_package(spdlog REQUIRED)
endif()

include_directories(lib)

add_subdirectory(lib)
add_subdirectory(MainServer)
#add_subdirectory(ViceServer)
add_subdirectory(Client)

add_custom_target(ctags
	WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
	COMMAND echo ${CMAKE_CURRENT_LIST_DIR}
	COMMAND ctags -R -h ".cc.cpp.h.proto" -o tags
	COMMENT
	"ctags successful create"
	VERBATIM
	)

message("CMAKE_CURRENT_SOURCE_DIR: " ${CMAKE_CURRENT_SOURCE_DIR})
message("CMAKE_CURRENT_LIST_DIR: " ${CMAKE_CURRENT_LIST_DIR})
message("CMAKE_CURRENT_BINARY_DIR: " ${CMAKE_CURRENT_BINARY_DIR})


